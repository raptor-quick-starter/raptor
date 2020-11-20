# raptor-quick-starter

An end-to-end test is a test that exercises an aspect of the system within the context of the system as a whole.

As an engineer, a product manager, a development lead, I would always want every critical aspect of the system to be tested as part of an end-to-end test. I just wouldn't live without this. This test not only verifies that the feature works, but it also verifies that it works under typical operational conditions. The end-to-end test is essential. I want to know that the system I'm delivering meets the requirements and will continue to meet the requirements as the system evolves in the future.

In the Testing Trophy, there are 4 types of tests.

End to End: A helper robot that behaves like a user to click around the app and verify that it functions correctly. Sometimes called "functional testing" or e2e.
Integration: Verify that several units work together in harmony.
Unit: Verify that individual, isolated parts work as expected.
Static: Catch typos and type errors as you write the code.

The biggest challenge so far is writing an E2E test for custom webcompoents (Polymer, Lit-html) having shadow DOM.

**Raptor-tests** has capability to easily test webcomponents just bu configuring few steps in a test script.

End to end test cases are nothing but a journey of login, few clicks, some inputs, navigations, some expected value of headings and finally logout.

One sample test script of Raptor


***** Detailed explanation of all the fields in test json scripts

1) **stepName**	Any string that will clearly explain the step which is currently being executed	
2	**action**	navigate, click, scroll, clickByText, input, sendKeys, expect	
3)	**time**	1000, 2000, 3000, 4000, Any value in milliseconds that is required to wait for next action before current action	
4)	**locator**	
document.querySelector("#screen-state").shadowRoot.querySelector("#form > form > button"),
login.submit.button

5)	**optionalLocator**	
document.querySelector("#screen-state").shadowRoot.querySelector("#form > form > button"),
login.submit.button
OptionalLocator is very useful when we are not sure of next possible button out two possibilities. One may come or second may come still test should pass

eg: while doing an action we may get one screen or we may get another screen. so it will be able to handle this scenario,

6)	**url**	https://www.abc.com/,
7)	**elementTextToFind**	"Mri Doctor" , Any text that we want to check if exist (with action clickByText) and click	
8)	**value**	2000,- 2000 (with action scroll),	
9)	**inputValue**	"Any String" (with action input),	
10	**optionalStep**	true, false, empty	
optionalStep is very useful when we are not sure if we will get that screen altogether or not, eg :

11	**expectedText**	"Doctor" Any text that we want to check if exist or not	
12	**sendKeys**
"Any value"	send keys is very helpful when we want to trigger on-blur option after entering values so that a disabled button will get enable before clicking it

Raptor can also be extended to selenium grid and Jenkins to trigger it via Job and send notification on success/failures :

Steps to add Selenium grid :

1) add these configurations to application.properties file and then read them in the test cases

app.isGridDisabled=true/false

app.gridNodeurl=https://{yourteamname}:{yourteamtoken}@seleniumgrid.abc.def:{port}/wd/hub

app.baseUrl=https://www.abc.com/

app.proxyUrl=http://proxy.abc.def.net:{port}

app.relativeTestscriptPath=src/test/resources/test-scripts/

app.relativescriptfailureScreenPath=target/surefire-reports/screenshot/error-

quitBrowserAfterTest=true

screenShotOnSuccess=false

app.defaulActionTime = 0

app.defaultWaitForOptionalSteps = 10

app.defaultTimeOut = 20

app.defaultBrowser = Chrome

app.browserVesrion = 85

chromeDriverPath =src/test/resources/drivers/chromedriver5

edgeDriverPath =
ieDriverPath =

One Sample test script:

  
{
  "testCaseConfig": {
    "testName": "Test Mri scan",
    "proxy": false,
    "browser": "Chrome"
  },
  "testSteps": [
    {
      "stepName": "navigate to url",
      "action": "navigate",
      "url": "https://www.alodokter.com/"
    },
    {
      "stepName": "click Cari Dokter",
      "action": "click",
      "locator": "anchorLocator"
    },
    {
      "stepName": "click mri scan",
      "action": "click",
      "locator": "mriScan"
    },
    {
      "stepName": "click Doktor",
      "action": "click",
      "locator": "document.querySelector(\"#elCardList > slider-tab-menu\").shadowRoot.querySelector(\"#dokter\")"
    },
    {
      "stepName": "input value",
      "action": "input",
      "locator": "document.querySelector(\"#filterProcedure\").shadowRoot.querySelector(\"#inputFilter\")",
      "inputValue": "Mri"
    }
  ]
}
