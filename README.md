# QA-Testing

const {test, expect} = require ('@playwright/test')

test('LoginFailed',async({browser})=>{
    const context = await browser.newContext();
    const page = await context.newPage();

  await page.goto("https://magento.softwaretestingboard.com/")
  await page.waitForLoadState('networkidle');

  await page.waitForTimeout(2000)
    const Signin = await page.locator("(//a[contains(text(),'Sign In')])[1]")
    const Email = await page.locator("#email")
    const Password = await page.locator("(//input[@id='pass'])[1]")
    const Submit = await page.locator("(//button[@id='send2'])[1]")
    const Required = await page.locator("(//div[@class='field email required'])[1]")

  //Login without input password
    await Signin.click()
    await Email.fill("hahacorp@mail.com")
    await Password.fill("")
    await Submit.click();

   await page.waitForSelector('.mage-error');
   
   const ErrorPass = await page.textContent('#pass-error'); //validasi text / required error
    console.log("Error Password: "+ErrorPass) 
    await page.waitForTimeout(2000)

  //Login without input email
    await Email.clear()
    await Email.fill("")
    await Password.fill("INIPASS")
    await Submit.click();
    await page.textContent('#email-error');
    
  await page.waitForTimeout(2000)

   //Login without input data
    await Email.clear()
    await Password.clear()
    await Email.fill("")
    await Password.fill("")
    await Submit.click();

   await page.textContent('#pass-error');
   await page.textContent('#email-error');
   
await page.waitForTimeout(3000)
   
})

test('ForgetPassword',async({browser})=>{
    const context = await browser.newContext();
    const page = await context.newPage();
    await page.waitForTimeout(3000)
    await page.goto("https://magento.softwaretestingboard.com/")
    await page.waitForLoadState('networkidle');

  const Signin = await page.locator("(//a[contains(text(),'Sign In')])[1]")
   await Signin.click();

  await page.locator("(//span[contains(text(),'Forgot Your Password?')])[1]").click();
   await page.locator("#email_address").fill("opp@mail.com")
  await page.locator("(//span[normalize-space()='Reset My Password'])[1]").click();

   await page.waitForSelector('.messages')

  const SuccessReset = await page.textContent("(//div[@class='message-success success message'])[1]")
    console.log("Wording Success: "+SuccessReset);

})

test('LoginSuccess',async({browser})=>{
    const context = await browser.newContext();
    const page = await context.newPage();
    await page.waitForTimeout(3000)
    await page.goto("https://magento.softwaretestingboard.com/")
    await page.waitForLoadState('networkidle');
    
  const Signin = await page.locator("(//a[contains(text(),'Sign In')])[1]")
    const Email = await page.locator("#email")
    const Password = await page.locator("#pass")
    const Submit = await page.locator("#send2")
    
   
  await Signin.click();
    await Email.fill("opp@mail.com")
    await Password.fill("Haechan06")
    await Submit.click();
    
   await page.waitForTimeout(3000)
})
