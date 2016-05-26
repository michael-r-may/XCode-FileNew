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

...

### When to submit youe first version
I would try to submit something to TestFlight as soon as you are able. This will not only help reassure you that the app is likely to pass review (but not guarantee) and show your beta testers what you are thinking/building but also get you into the habit of doing app submissions. 
