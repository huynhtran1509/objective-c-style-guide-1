# NYTimes Objective-C Style Guide

ဒီ style guide သည် [NY Times](https://github.com/NYTimes/objective-c-style-guide) iOS Team မှ အသုံးပြုသော style guide ဖြစ်သည်။

## Introduction

အောက်ပါတို့ သည် Apple မှ ရေးသားပြထားသော style guide အချို့ဖြစ်သည်။

* [The Objective-C Programming Language](http://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/ObjectiveC/Introduction/introObjectiveC.html)
* [Cocoa Fundamentals Guide](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CocoaFundamentals/Introduction/Introduction.html)
* [Coding Guidelines for Cocoa](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/CodingGuidelines.html)
* [iOS App Programming Guide](http://developer.apple.com/library/ios/#documentation/iphone/conceptual/iphoneosprogrammingguide/Introduction/Introduction.html)

## Table of Contents

* [Dot-Notation Syntax](#dot-notation-syntax)
* [Spacing](#spacing)
* [Conditionals](#conditionals)
  * [Ternary Operator](#ternary-operator)
* [Error handling](#error-handling)
* [Methods](#methods)
* [Variables](#variables)
* [Naming](#naming)
  * [Underscores](#underscores)
* [Comments](#comments)
* [Init & Dealloc](#init-and-dealloc)
* [Literals](#literals)
* [CGRect Functions](#cgrect-functions)
* [Constants](#constants)
* [Enumerated Types](#enumerated-types)
* [Private Properties](#private-properties)
* [Image Naming](#image-naming)
* [Booleans](#booleans)
* [Singletons](#singletons)
* [Xcode Project](#xcode-project)

##Dot-Notation Syntax

Properties တွေအတွက် dot-notation ကို အမြဲ အသုံးပြုပါ။ Instances အတွက် bracket notation ကို အသုံးပြုပါ။

ဥပမာ

```objc
view.backgroundColor = [UIColor orangeColor];
[UIApplication sharedApplication].delegate;
```

ဒီလို မသုံးပါနှင့်

```objc
[view setBackgroundColor:[UIColor orangeColor]];
UIApplication.shareAppliaction.delegate;
```

##Spacing

- Indent အတွက် 4 spaces ကို အသုံးပြုမည်။ Tabs ကို အသုံးမပြုပါ ။ Xcode preference ကို ပြင်ထားဖို့လိုသည်။
- Method braces နှင့် အခြား brances (`if` / `else`/`switch`/`while`) စသည်တို့ကို open အတွက် same line တွင် အသုံးပြုမည်ဖြစ်ပြီး close ကို new line မှာ အသုံးပြုမည်။

ဥပမာ

```objc
if (user.isHappy) {
//Do something
}
else {
//Do something else
}
```

- method တစ်ခု နဲ့ တစ်ခုကြား blank လိုင်း တစ်ခု ထားပေးရမည်။ သို့မှသာ ထင်ရှားစွာ မြင်တွေ့နိုင်မည်။
- `@synthesize`နှင့် `@dynamic` စသည်တို့ကို လိုင်း အသစ်တွေ ရေးသားရမည်။

##Conditionals

Conditional ရဲ့ body ဟာ အမြဲတန်း အဖွင့် နှင့် အပိတ်ကို အသုံးပြုမည်။ အဖွင့် အပိတ် မပါခြင်း (လိုင်းတစ်ကြောင်း တည်းရေးခြင်း) ကို အသုံးမပြု။ တစ်ကြောင်းတည်း အသုံးပြုခြင်းသည် [အန္တရာယ်](http://programmers.stackexchange.com/questions/16528/single-statement-if-block-braces-or-no/16530#16530) ရှိသည်။ လက်ရှိ style guide တွင် လွယ်ကူစွာ ဖတ်ရှုနိုင်ရန် အဖွင့် နှင့် အပိတ်ကို မဖြစ်မနေ အသုံးပြုရမည်။

ဥပမာ

```objc
if (!error) {
    return success;
}
```

ဒီလို မရေးပါ

```objc
if (!error)
    return success;
```

ဒါမှမဟုတ်

```objc
if (!error) return success;
```

###Ternary Operator

Ternary operator, ? , တို့ကို ရှင်းရှင်းလင်းလင်း ရေးသင့်သည်။ conditin တစ်ခု တည်း ကို သာ အသုံးပြုသင့်သည်။ multiple conditions များသည် နားလည်ရခက်ပြီး variable များ ရှုပ်ထွေးနိုင်သောကြောင့် ဖြစ်သည်။

ဥပမာ

```objc
result = a > b ? x : y;
```

ဒီလို မရေးပါ

```objc
result = a > b ? x = c > d ? c : d : y;
```


## Error handling

error variable ကို အသုံးမပြုပါ။ error ကို by reference ဖြင့် အသုံးပြုသည်။

ဥပမာ

```objc
NSError *error;
if (![self trySomethingWithError:&error]) {
    // Handle Error
}
```

ဒီလို မဟုတ်ပါ။

```objc
NSError *error;
[self trySomethingWithError:&error];
if (error) {
    // Handle Error
}
```

## Method

Method မာျးကို (-/+ symbol) ပြီးလျှင် space ခြားသည်။ method segment ကြားတွင်လည်း space ခြားသည်။

ဥပမာ

```objc
- (void)setExampleText:(NSString *)text image:(UIImage *)image;
```

## Variable

Variable name တွေဟာ အတတ်နိုင်ဆုံး အဓိပ္ပာယ်ပြည့်ဝ အောင် ရေးသားဖို့လိုပါတယ်။ Single letter varialble name တွေကို `for()` loop မှ လွဲ ၍ အသုံးမပြုပါ။

Asterisks ကို varialble ၏ ရှေ့တွင် ရေးသားပါသည်။ ဥပမာ `NSString *text` ဒီလို အသုံးမပြုပါ `NSString* text` ဒါမှမဟုတ် `NSString * text` 

Property definitations တွေမှာ naked instance varialble ကို ဖြစ်နိုင်လျှင် အသုံးပြုပါ။ 

ဥပမာ 

```objc
@interface NYTSection: NSObject

@property (nonatomic) NSString *headline;

@end
```

ဒီလို မဟုတ်ပါ။:

```objc
@interface NYTSection : NSObject {
    NSString *headline;
}
```

## Naming

Apple naming conventions ကို ဖြစ်နိုင်ရင် လေ့လာလိုက်နာသင့်သည်။ အထူးသဖြင့် [memory management rules](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/MemoryMgmt/Articles/MemoryMgmt.html) ([NARC](http://stackoverflow.com/a/2865194/340508)) နဲ့ ပတ်သက်တဲ့ အပိုင်းတွေကိုပေါ့။

ဥပမာ

```objc
UIButton *settingsButton;
```

ဒီလို မဟုတ်ပါ။

```objc
UIButton *setBut;
```

စာသုံးလို့ ကို ရှေ့မှာ ထားတဲ့ ပုံစံ ( ဥပမာ `NYT`) ကို class name ,constant တွေရဲ့ ရှေ့မှာ အသုံးပြုပါ။ Core Data entity names မှာ တော့ အသုံးမ​ပြုပါနဲ့။

ဥပမာ


```objc
static const NSTimeInterval NYTArticleViewControllerNavigationFadeAnimationDuration = 0.3;
```

ဒီလိုမရေးပါ။

```objc
static const NSTimeInterval fadetime = 1.7;
```

Properties တွေ အတွက် camel-case(စာလုံးကြီးအသေးအကြီး ပုံစံ) ကို အသုံးပြုပါမည်။ စတဲ့ စာလုံးကိုတော့ အသေးနဲ့ပဲစပါမယ်။ တကယ်လို့ Xcode က synthesize variable ကို အလိုအလျောက် generate လုပ်ပေးရင်တော့ ထားလိုက်ပါ။ မဟုတ်ခဲ့ရင်တော့ properties ကို camel-case အသုံးပြုပြီးတော့ synthesize အတွက် underscore စတာကို အသုံးပြုပါမယ်။

ဥပမာ

```objc
@synthesize descriptiveVariableName = _descriptiveVariableName;
```

ဒီလိုမရေးပါ။

```objc
id varnm;
```

### Underscores

Properties , instance variable ကို အသုံးပြုတဲ့ အခါမှာ `self` ကို အသုံးပြုပါ။ local variables တွေရဲ့ နာမည်မှာ underscores မပါသင့်ပါဘူး။

## Comments

comments တွေ ရေးဖို့လိုတဲ့ အခါမှာ **why** ကို ရှင်းပြပေးဖို့လိုပါတယ်။ comments အားလုံးတွေဟာ up-to-date ဒါမှမဟုတ် မရှိတော့တာတွေကို ဖျက်ထားပေးဖို့လိုပါတယ်။

Block comments ကို တတ်နိုင်လျှင် ရှောင်ရှားသင့်ပါတယ်။ code တွေဟာ self-documenting ဖြစ်ဖို့လိုပါတယ်။ စာကြောင်း အနည်းငယ်နဲ့ ရှင်းပြထားဖို့သာ လိုအပ်သည်။ ထိုရှင်းပြထားသည်များကို documentation generate လုပ်တဲ့ အခါတွင် အသုံးပြုမှာ မဟုတ်ပါဘူး။

## init and dealloc

`dealloc` methods တွေဟာ ထိပ်မှာ implementation လုပ်ထားဖို့လိုပါသည်။ `@synthesize` နှင့် `@dynamic` အပြီးတွင် ရေးဖို့လိုသည်။ `init` ဟာ class ရဲ့ `dealloc` method  အောက်တွင် ရေးဖို့လိုသည်။

`init` method သည် အောက်ပါ ပုံစံ ဖြစ်ရမည်။

```objc
- (instancetype)init {
    self = [super init]; // or call the designated initalizer
    if (self) {
        // Custom initialization
    }

    return self;
}
```

## Literals

`NSString`, `NSDictionary`, `NSArray`, နှင့် `NSNumber` တို့ကို imutable instance objects  တွေ ဖန်တီးတဲ့ အခါမှာ အသုံးပြုပါ။ `nil` value ကို `NSArray` နှင့် `NSDictionary` တို့၏ literals တွင် ထည့်သွင်းလို့ မရပါ။ crash ဖြစ်နိုင်သည်။

**ဥပမာ :**

```objc
NSArray *names = @[@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul"];
NSDictionary *productManagers = @{@"iPhone" : @"Kate", @"iPad" : @"Kamal", @"Mobile Web" : @"Bill"};
NSNumber *shouldUseLiterals = @YES;
NSNumber *buildingZIPCode = @10018;
```

**ဒီလို မသုံးပါနှင့်:**

```objc
NSArray *names = [NSArray arrayWithObjects:@"Brian", @"Matt", @"Chris", @"Alex", @"Steve", @"Paul", nil];
NSDictionary *productManagers = [NSDictionary dictionaryWithObjectsAndKeys: @"Kate", @"iPhone", @"Kamal", @"iPad", @"Bill", @"Mobile Web", nil];
NSNumber *shouldUseLiterals = [NSNumber numberWithBool:YES];
NSNumber *buildingZIPCode = [NSNumber numberWithInteger:10018];
```

## CGRect Functions


`CGRect` ရဲ့ `x`, `y`, `width`, သို့မဟုတ် `height` တို့ကို access လုပ်တဲ့ အခါမှာ direct struct ခေါ်မည့်အစား [`CGGeometry` functions](http://developer.apple.com/library/ios/#documentation/graphicsimaging/reference/CGGeometry/Reference/reference.html) ကို အသုံးပြုပါ။

Apple's `CGGeometry` reference တွင် ဖော်ပြထားသည်မှာ :

> All functions described in this reference that take CGRect data structures as inputs implicitly standardize those rectangles before calculating their results. For this reason, your applications should avoid directly reading and writing the data stored in the CGRect data structure. Instead, use the functions described here to manipulate rectangles and to retrieve their characteristics.


**ဥပမာ:**

```objc
CGRect frame = self.view.frame;

CGFloat x = CGRectGetMinX(frame);
CGFloat y = CGRectGetMinY(frame);
CGFloat width = CGRectGetWidth(frame);
CGFloat height = CGRectGetHeight(frame);
```

**ဒီလို မသုံးပါနှင့်:**

```objc
CGRect frame = self.view.frame;

CGFloat x = frame.origin.x;
CGFloat y = frame.origin.y;
CGFloat width = frame.size.width;
CGFloat height = frame.size.height;
```

## Constants

Constans တွေကို in-line string literals သို့မဟုတ် numbers အနေဖြင့် အသုံးပြုသင့်သည်။ search and replace လုပ်စရာမလိုပဲ value ကို လွယ်လင့်တကူ ပြောင်းလဲနိုင်ရန် အတွက် ဖြစ်သည်။ Constanst တွေကို `static` ကြေငြာပါ။ macro မှ လွဲ၍ `define` ကို ဖြစ်နိုင်လျှင် အသုံးမပြုပါနှင့်။  

**ဥပမာ :**

```objc
static NSString * const NYTAboutViewControllerCompanyName = @"The New York Times Company";

static const CGFloat NYTImageThumbnailHeight = 50.0;
```

**ဒီလို မသုံးပါနှင့် :**

```objc
#define CompanyName @"The New York Times Company"

#define thumbnailHeight 2
```

## Enumerated Types

When using `enum`s, it is recommended to use the new fixed underlying type specification because it has stronger type checking and code completion. The SDK now includes a macro to facilitate and encourage use of fixed underlying types — `NS_ENUM()`

**Example:**

```objc
typedef NS_ENUM(NSInteger, NYTAdRequestState) {
    NYTAdRequestStateInactive,
    NYTAdRequestStateLoading
};
```

## Private Properties

Private properties should be declared in class extensions (anonymous categories) in the implementation file of a class. Named categories (such as `NYTPrivate` or `private`) should never be used unless extending another class.

**For example:**

```objc
@interface NYTAdvertisement ()

@property (nonatomic, strong) GADBannerView *googleAdView;
@property (nonatomic, strong) ADBannerView *iAdView;
@property (nonatomic, strong) UIWebView *adXWebView;

@end
```

## Image Naming

Image names should be named consistently to preserve organization and developer sanity. They should be named as one camel case string with a description of their purpose, followed by the un-prefixed name of the class or property they are customizing (if there is one), followed by a further description of color and/or placement, and finally their state.

**For example:**

* `RefreshBarButtonItem` / `RefreshBarButtonItem@2x` and `RefreshBarButtonItemSelected` / `RefreshBarButtonItemSelected@2x`
* `ArticleNavigationBarWhite` / `ArticleNavigationBarWhite@2x` and `ArticleNavigationBarBlackSelected` / `ArticleNavigationBarBlackSelected@2x`.

Images that are used for a similar purpose should be grouped in respective groups in an Images folder.

## Booleans

Since `nil` resolves to `NO` it is unnecessary to compare it in conditions. Never compare something directly to `YES`, because `YES` is defined to 1 and a `BOOL` can be up to 8 bits.

This allows for more consistency across files and greater visual clarity.

**For example:**

```objc
if (!someObject) {
}
```

**Not:**

```objc
if (someObject == nil) {
}
```

-----

**For a `BOOL`, here are two examples:**

```objc
if (isAwesome)
if (![someObject boolValue])
```

**Not:**

```objc
if ([someObject boolValue] == NO)
if (isAwesome == YES) // Never do this.
```

-----

If the name of a `BOOL` property is expressed as an adjective, the property can omit the “is” prefix but specifies the conventional name for the get accessor, for example:

```objc
@property (assign, getter=isEditable) BOOL editable;
```
Text and example taken from the [Cocoa Naming Guidelines](https://developer.apple.com/library/mac/#documentation/Cocoa/Conceptual/CodingGuidelines/Articles/NamingIvarsAndTypes.html#//apple_ref/doc/uid/20001284-BAJGIIJE).

## Singletons

Singleton objects should use a thread-safe pattern for creating their shared instance.
```objc
+ (instancetype)sharedInstance {
   static id sharedInstance = nil;

   static dispatch_once_t onceToken;
   dispatch_once(&onceToken, ^{
      sharedInstance = [[self alloc] init];
   });

   return sharedInstance;
}
```
This will prevent [possible and sometimes prolific crashes](http://cocoasamurai.blogspot.com/2011/04/singletons-your-doing-them-wrong.html).

## Xcode project

The physical files should be kept in sync with the Xcode project files in order to avoid file sprawl. Any Xcode groups created should be reflected by folders in the filesystem. Code should be grouped not only by type, but also by feature for greater clarity.

When possible, always turn on "Treat Warnings as Errors" in the target's Build Settings and enable as many [additional warnings](http://boredzo.org/blog/archives/2009-11-07/warnings) as possible. If you need to ignore a specific warning, use [Clang's pragma feature](http://clang.llvm.org/docs/UsersManual.html#controlling-diagnostics-via-pragmas).

# Other Objective-C Style Guides

If ours doesn't fit your tastes, have a look at some other style guides:

* [Google](http://google-styleguide.googlecode.com/svn/trunk/objcguide.xml)
* [GitHub](https://github.com/github/objective-c-conventions)
* [Adium](https://trac.adium.im/wiki/CodingStyle)
* [Sam Soffes](https://gist.github.com/soffes/812796)
* [CocoaDevCentral](http://cocoadevcentral.com/articles/000082.php)
* [Luke Redpath](http://lukeredpath.co.uk/blog/my-objective-c-style-guide.html)
* [Marcus Zarra](http://www.cimgf.com/zds-code-style-guide/)
