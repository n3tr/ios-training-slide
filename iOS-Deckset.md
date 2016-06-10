
# Introduction to iOS

---

## Setup

- Xcode
- Cocoapods
- Git

---

## Topic

- Basic Objective
  - Types
  - Class
  - Object
  - Properties
- Interface Builder
- View
- View Controller

---

## Objective-C

---

### This page intentionally to be

## `nil`

---

### Types

---

### Primitive

---

**Number**

```objc
int i = 100;
NSInteger i = 10000;
```

**Boolean**

```objc
BOOL isLoading = YES;
BOOL isDone = NO;
```
---

### Reference

**NSObject**

- Base class for all Objective-C classes

---

**String**

```objc
NSString *myString = @“hello”

NSString *myString = [otherString stringByAppendingString:yetAnotherString]

NSString *myString = [NSString stringWithFormat:@“%d%@”, myInt, myObj]
```
---

**Array**

```objc
// prefer
NSArray *heroes = @[@"Windrunner", @"Sven", @"LifeStealer"];
heroes[0] // --> "Windrunner"
```

---

**Mutable Array**

```objc
NSMutableArray *heroes = [NSMutableArray new];
[heroes addObject:@"Windrunner"];
[heroes objectAtIndex:0]; // --> "Windrunner"
heroes[0] // --> "Windrunner"
```

---

**NSNumber**

Generic number-holding class

```objc
// Old Style
NSNumber *num = [NSNumber numberWithInteger:2];
NSNumber *num = [NSNumber numberWithBool:YES];

// New Literal
NSNumber *num = @1;
NSNumber *num = @YES;

// Convert Back
[num intergerValue]; // 1 or YES
```

---



**NSDate[^1]**

```objc
NSDateFormatter *dateFormatter = [[NSDateFormatter alloc] init];
[dateFormatter setDateStyle:NSDateFormatterMediumStyle];
[dateFormatter setTimeStyle:NSDateFormatterNoStyle];

NSDate *date = [NSDate dateWithTimeIntervalSinceReferenceDate:162000];

NSString *formattedDateString = [dateFormatter stringFromDate:date];
NSLog(@"formattedDateString: %@", formattedDateString);
// Output for locale en_US: "formattedDateString: Jan 2, 2001".
```



[^1]: NSDate further reading: https://developer.apple.com/library/ios/documentation/Cocoa/Conceptual/DataFormatting/DataFormatting.html

---

**id**

pointer to an object of unknown/unspecified” type.

```objc
NSString *s = @“x”;
id obj = s;
NSArray *a = obj;
```

---

### Class

There're common 2 files when create Class.

`JKPerson.h` - *Header files*

- The Interface for a Class Defines Expected Interactions

`JKPerson.m` - *Implementation file*

- The Implementation of a Class Provides Its Internal Behavior

---

### Class Example

---

`JKPerson.h`

```objc
// JKPerson.h
@interface JKPerson : NSObject


// Properties
@property (nonatomic, copy) NSString *firstName;
@property (nonatomic, copy) NSString *lastName;
@property (nonatomic, readonly) NSDate *birthday
@property (nonatomic, assign, getter=isRobot) BOOL robot;

// Methods
- (NSString *)getFullName;
- (void)sayTo:(XYZPerson *)otherPerson withMessage:(NSString *)message;

@end
```

---

`JKPerson.m`

```objc
#import "JKPerson.h"

@implementation JKPerson

- (NSString *)getFullName
{
  return [NSString stringWithFormat@"%@ %@", self.firstName, self.lastname];
}

// ...

@end
```

---

### Object

**Object Creation**

```objc
// Object Creation
JKPerson *person = [JKPerson new];

// Property accessor
NSString *name = person.firstName;

// Property assign
person.firstName = @"Net";
```

---

**Method Call**

```objc
JKPerson *person = [JKPerson new];

NSString *fullName = [person getFullName];

[person sayTo:otherPerson withMessage:@"Hello"];
```

---

### Getter / Setter

Property will be generate Getter / Setter method by default

```objc
@property (nonatomic, copy) NSString *firstName;
```

Code below will be generated

```objc
-(NSString *)firstName
{
  return _firstName;
}

-(void)setFirstName:(NSString *)firstName
{
  _firstName = firstName;
}

**Note: Why `_firstName` not `self.firstName`**
```

---

### self.firstName vs _firstName

`_firstName`: will access directly to instance variable
`self.firstName`: will access via getter / setter method

---

```objc
self.firstName = @"Net";
// equivalent to
[self setFirstName:@"Net"]
```

and

```objc
NSString *name = self.firstName;
// equivalent to
NSString *name = [self firstName];
```

---

## Object Ownership

### Strong / Weak / Copy / Assign

#### Let's talk about balloon


---

# UIView

## Let's Play Together!!

---

# View Controller

---

### View Controller Life Cycle

```objc
- (void)loadView;
- (void)viewDidLoad; // **
- (void)viewWillAppear:(BOOL)animated; // **
- (void)viewDidAppear:(BOOL)animated;
- (void)viewWillDisappear:(BOOL)animated; // **
- (void)viewDidDisappear:(BOOL)animated;
```

---

### Delegate / Protocol

---

### Protocol

Looks a lot like @interface (but there’s no corresponding @implementation)

```objc
@protocol Foo

@property (readonly) int readonlyProperty;
@property NSString *readwriteProperty;

@required
- (void)someMethod;

@optional
- (void)methodWithArgument:(BOOL)argument;
- (int)methodThatReturnsSomething;

@end
```

---

### Protocol (cont)

```objc
// MyClass.h
#import “Foo.h”
@interface MyClass : NSObject <Foo>
  // ...
@end
```

```objc
// MyClass.m
@imeplement MyClass

- (void)someMethod
{
  // do something
}

@end
```

---

### Data Storage

- **NSUserDefault**
- CoreData
- Sqlite

---
