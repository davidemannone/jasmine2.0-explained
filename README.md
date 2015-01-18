# jasmine2.0-explained
Jasmine.js 2.0 and DelinitelyTyped that allows failure messages

So many discussions and closures for just introducing an explanation string when an expectation fails! 
Ok, that BDD tests can be made perfecty whith just the describe-it paradigm but what breaks if we provide a fail message when someone needs it and so use a describe-it-accuratly form? When not necessary, just do not set it!

I find this issue really usefull and error tracking is more efficient and less time consuming, despite the fact to set your tests in the proper BDD form.

So I made for myself the changes I needed to provide the way I jugded right to implement this usefull feature following many proposals I found and finally I decided to provide it here. 
I've used jasmine 2.0 because it's the last one that has also the definitely typed jasimine.d.ts. I don't know when and if I will do the same changes for the jasmine's 2.1. I'm using right now TypeScript and I should realize a completely new release of the corresponding ts description file and I do not need it for now.  

I should have introduced the new custom features right up the entire Jasmine framework without introducing, I hope, any significant modification. I made some test but just relatively to the machers I'm using and it works fine. I don't now what happens with other part I havent'used it until today (and I don't want to discover it for know). Apart from the custom messaging system I've introduced I've got also a "positive" but maybe not so usefull side effect that could be used anywhere (I do it sometimes). 
Meanwhile I discovered also there is a matching error in the official definitely typed versione available! But sincerely it is nothing important and right a wrong return type of the matchers that are declared as returning boolean even if the js version do not provides any return value. But who is using an: if (expect(XXX).toBe(YYY))? 

Sorry if I haven't directly forked-and-modified the 2.0 branch, but for my purposes and maybe yours, I felt it easier just overriding 2 files! All lines I've modified are marked-commented strating with // CUSTOM CHANGE, followed by a brief description of the purpose of the change I made.

Mi custom changes provide to you this now:

1. If you do not provide anything all is exactly as before
2. Any matcher can know be followed by the new default descriptor I've included: byFailReport("message") or byFailReport(message: string) if you use TS.
3. As the function says, your custom message will be reported only if the preceding matcher has failed.
4. This is a typical use: expect(SOMETHING).toEqual(WHAT-EXPECTED).byFailReport("YOUR-CUSTOM-REPORT!");
5. If the matcher succeeds nothing is displayed as before
6. If the matcher fails the report diplays now (continuing the above example): "Expected SOMETHING to be WHAT-EXPECTED. >YOUR-CUSTOM-REPORT!< 
7. You can now link an arbitrary number of matcher toghether forming one single expectating sentence like this: expect(SAY-AN-OBJECT.SAY-A-PROPERTY).toBeDefined().toEqual(EXPECTED-VALUE)
8. from the above you can so write: expect(SAY-AN-OBJECT.SAY-A-PROPERTY).toBeDefined().byFailReport("MISSING...").toEqual(EXPECTED-VALUE).byFailReport("WRONG...")
9. I do not have broken the evaluation chain if some failure happens before, so that all matchers can be evaluated properly, and so report to you all of what is expected to be right.
10. The not matcher behaves ad before. In an evaluation chain it belongs just to the following matcher. As example: expect(SAY-AN-OBJECT).not.toBe(THISOBJ).byFailReport("IS THISOBJ").toBe("THATOBJ").byFailReport("BUT NOT THATOBJ")
11. I've mantained subsequent calls byFailReport's messages to be connected toghether if the preceding matcher fails: expect(SOMETHING).toEqual(WHAT-EXPECTED).byFailReport("YOU FAILED!").byFailReport("OH YES!") would report: >OH YES!< >YOU FAILED!< ... 
12. I do not have testest the ANY macher nor many others. As soon I'll use they I will fix the possible bugs and report here the update. Or let me know with an example what goes wrong and I will do my tests.
13. Maybe better: mae the changes from your own and then report it directly here!


How to use it: just download jasmine.js and/or jasmine.d.ts and replace it in place of yours original ones.

