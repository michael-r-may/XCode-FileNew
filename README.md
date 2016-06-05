# Xcode-FileNew
Considerations, suggestions and recommendations for when starting a new iOS project

## Why
Very soon I will be starting a new job, with a brand new app. So, for the first time in years I will be hitting the hallowed menu option ```File > New``` in Xcode. With that in mind, I wanted to start thinking about what I've learned along the way that might inform my choices this time, as well as source the same kind of knowledge from the community. 

To my suprise no document seemed to exist that distilled any of this kind of knowledge (I may well be wrong, I didn't search all that hard) and so I decided to make this and see what happens next.

I will begin putting my own thoughts in here, but if you find it useful, or disagree, or see something you cannot believe I missed out, pull requests are very welcome.

And so, without further ado..let us begin

## Project or Workspace?
A workspace, containing the new project, is often a better choice if you think you will be using CocoaPods or have other dependencies that you would like to see within Xcode Project Navigator, and build alongside the main project. You can certainly postpone this decision until later, and just use a project if you want, but I like having this set up from day one so I don't have to retrain myself to open the ```myapp.xcworkspace``` instead of the ```myapp.xcodeproj```.

### Which Template?
It's unlikely that any of them will be quite what you want out of the box, but it will certainly make life easier to pick the one that most closesly aligns with your expected app design. If you are unsure, I would go with with Single View Application and build up from there.

### Product Name and Organization Name
You are on your own here - only you will know what these should be. Choose names that you expect to appear on the app store and, remember, check the Apple Guidelines if you are unsure. Certainly avoid using names that you do not own, or which appear to be other apps, or which appear to be companions to other apps. [Coat tail riding](http://idioms.thefreedictionary.com/ride+coattails) is not cool and will probably get you rejected on submission.

### Organization Identifier
This will form the prefix of your Bundle Identifier and is typically a reverse domain name. For example ```com.mydomain``` will be combined with your product name (say, ```MyApp```) to form the bundle identifier ```com.mydomain.MyApp```.

### Bundle Identifier
This will be created by Xcode, for you, from the product name and bundle identifier.

### Language
I would assert that, unless you have a good reason to believe otherwise, Swift is the only option for a brand new project. There may be reasons not to, but given you can bridge back to Objective-C if you need to, the reasons so start a project in Objective-C are small.

### Devices
This probably needs a discussion with the wider team; from the product manager, designer and possibly others, the implications of going Universal (my recommendation) from the start are too big to not consider in advance. But, if you can embrace autolayout and a Universal app, you will avoid back-loading your development effort when you decide one day to support the iPad too. That being said, the effort of designing, and testing, for multiple form factors should not be underestimated.

### Use Core Data
If you don't need Core Data on day one, I would avoid ticking this and retrofit it later. And then, of course, there is the fact that the boiler plate code is huge, and ends up all in your AppDelegate. Which is ugly, wrong and well, just ugly and wrong will do fine.  

### Include Unit Tests
You can add a unit testing target later, with relative ease, so this is not an all-or-nothing decision either, but I would suggest that merely having the target there will help coax you into writing tests. Nature, and developers, abhore a void and an empty test target is a void of disapproval.

### Include UI Tests
Whilst nothing like as stable, especially when in a CI environment, I would tick this box too and try to get a few of your core journeys working reliably on your own machine at least. That way you can hit [cmd+u](https://developer.apple.com/library/mac/recipes/xcode_help-test_navigator/RunningTests/RunningTests.html) before you run off to to lunch and have that warm fuzzy feeling before you later hit [Submit](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/SubmittingYourApp/SubmittingYourApp.html).

...

### Autolayout
When Autolayout was first introduced it was Apple's way of telling us that different screensizes were coming (and that they regretted not having this ready for the iPad, I propose) and come they did. If you are still holding out, making do with springs and struts and all that layoutSubviews fun, then this is your chance to embrace the bright new future of constraints. Sure it will bite you from time to time, and the learning curve up is going to be a headache but you'll end up writing much less code and, in most cases, it will just work. 

Assuming your team also agree with the compromise, you can even ship for iPad and iPhone from one codebase, and one xib/storyboard on day one. Sure it'll be a compromise, looking for all the world like a big iPhone app (because it is) but it's a lot less ugly than the iPhone app running at 2x magnification. I find it helps smash the phone versus tablet thinking too (where does a 6 Plus fit in?) and means no retrofitting later. Instead of wasting time making it work on iPads you can spend that time making it work _better_ on iPads.

Apple also insist your [app must work on the iPad even if you design for iPhone](https://developer.apple.com/app-store/review/guidelines/#functionality) and will reject you if not so, really, just start out doing the right thing (tm) and sleep easier.

### Code Coverage
You've added the unit and UI test targets right? So why would you _not_ want to know where your coverage is best, and weakest? Exactly.

### Enable Bitcode (ENABLE_BITCODE)
TBC

### Treat Warnings As Errors (GCC_TREAT_WARNINGS_AS_ERRORS)
If you turn this on before you write a single line of code, your app will still compile without problem. Then you get to feel all ninja/god/rockstar/jedi/whatever-stokes-your-ego that you [turned things up to 11](https://en.wikipedia.org/wiki/Up_to_eleven). 

### Warn about four-char literals (GCC_WARN_FOUR_CHARACTER_CONSTANTS)
As the description says 'Warn about four-char literals (e.g., MacOS-style OSTypes: 'APPL')'. Just check the box already and know you won't ever collide with a reserved OSType and live to regret it.

### Hidden Local Variables (GCC_WARN_SHADOW)
I would enable this. It's really not a good idea to have variables shadowing each other, as it makes reasoning about your code that much harder and, as well all know, 'Programs must be written for people to read, and only incidentally for machines to execute' - [Abelson & Sussman](http://www.amazon.com/dp/0262011530/ref=cm_sw_r_tw_dp_Ji1rxb0PAR08G)

### Incorrect Uses Of Nullable Values (CLANG_WARN_NULLABLE_TO_NONNULL_CONVERSION)
Ask yourself why you wouldn't want to know if you misused the ```_Nonnull``` (for example) and then go enable this.

### Initializer not fully bracketed (GCC_WARN_INITIALIZER_NOT_FULLY_BRACKETED)
Sure, it's a minor issue, and highly unlikely to cause problems, but you're about to start your [Sistine Chapel](https://en.wikipedia.org/wiki/Sistine_Chapel) project so why would you let a future viewer of your masterpiece spot an angel with only four fingers (when the computer can tell you first).

### Out-of-Range Enum Assignments (CLANG_WARN_ASSIGN_ENUM)
Enable this. You've created an enum for a reason, so accidentally using values outside of it must surely be something you want to know about?

### Analytics
As certain as taxes, these are my facts about Analytics; If you don't have them, you will one day be asked about them and have to retrofit them. If you do have them, you will one day be asked about some you don't have, and have to retrofit them. If you have them, and plentifully, you will one day be asked to switch provider, and have to retrofit it. 

The good news is that you can get a lot, for free, and with little or no coding effort. In the no coding camp is [Apple Analytics](https://analytics.itunes.apple.com/), which have come a very long way since they first went live. These will be very valuable when you launch so get used to how they work, and what they can tell you right now (you might want to stufy the stuff around sources and campaigns, for example).

Additionally for a small amount of effort you can get deeper insight with the likes of [Crashlytics](http://try.crashlytics.com/). As the name suggests you can get real-time, prioritised, crash logs from this company (this is now owned by Twitter). They now offer additional services, like analytics events and near real-time reporting on user numbers (which is almost hypnotising).

For greater power, and greater expense, there is [MixPanel](https://mixpanel.com/). I've not used this, but I know others who have and they love it. Being able to tie a push notification to an analytics event (or it's absence), for example, can be very powerful in re-engaging users, without having to write custom code.

Once upon a time [Flurry](https://developer.yahoo.com/analytics/) was the top dog in the app analytics world. Then people started really innovating and they did not. Yahoo now owns them (but that's about all that has changed recently).

Now, as I said, it's likely you'll end up changing analytics during the life of your app, and this is a huge pain if you don't plan for it. The answer, of course, is abstraction. Thankfully, Orta already realised this and has written an abstraction layer called [ARAnalytics](https://github.com/orta/ARAnalytics).

If you want to roll your own, go for it. Just remember to keep it nice and abstract.

### Crash Reporting
TBC: Crashlytics, Apple Crash Reporting

### Push Notifications
TBC: 

### Fastlane
TBC: 

...

### When to use feature toggling
TBC: 

### A/B Testing
TBC: 

### When to submit your first version
I would try to submit something to TestFlight as soon as you are able. This will not only help reassure you that the app is likely to pass review (but not guarantee) and show your beta testers what you are thinking/building but also get you into the habit of doing app submissions. 

### Using Rate This App prompts
TBC: 
