#AOHome - Out of the box home application

AOHome is under MIT Licence so if you find it helpful just use it !

###**AOHomeDemo**

This project add/remove tag with image and title inside a tag list view. When user tap on a tag, it's removed from the view. Please see the sample project for more.

The AOMedallionView inherit from AGMedallionView library to add user interaction and delegate method available.

https://github.com/arturgrigor/AGMedallionView.git

###**Screenshot:**
AOHomeDemo in the iphone simulator

![AOHomeDemo in the simulator][1]

##How To Use It

Sample project show a simple usage.

###Documentation

```objc

@protocol AOHomeViewControllerDelegate <NSObject>

/**
 * Called when a new profile medallion is being tapped
 */

- (void)newMedallionTapped;

/**
 * Called when a medallion is being tapped
 */

- (void)medallionTappedWithUserInfo:(id)userInfo;

@end

/**
 * Custom init method to create a new AOHomeViewController object
 *
 * @param NSTimeInterval background image pan effect duration
 * @param NSUInteger background image pan effect size
 * @param NSArray collection of background images defined with images bundle name (ie. @[@"bg_1.jpg", @"bg_2.jpg", @"bg_3.jpg"])
 *
 * @return AOHomeViewController
 */

- (instancetype)initWithPanDuration:(NSTimeInterval)panDuration withPanSize:(NSUInteger)panSize andBackgroundImages:(NSArray *)images;

/**
 * Add a medallion 
 *
 * @param UIImage medallion image
 * @param NSString medallion title
 * @param BOOL new profile medallion
 * @param id some information to be used
 */

- (void)addMedallionWithImage:(UIImage *)anImage andTitle:(NSString *)aTitle newProfile:(BOOL)isNewProfile userInfo:(id)userInfo;

/**
 * Hide all medallion
 *
 * @param NSTimeInterval a duration for the fade out
 * @param NSTimeInterval a delay to start the fade out
 */

- (void)hideProfilsWithDuration:(NSTimeInterval)aDuration afterDelay:(NSTimeInterval)aDelay;

/**
 * Show all medallion
 *
 * @param NSTimeInterval a duration for the fade in
 * @param NSTimeInterval a delay to start the fade in
 */

- (void)showProfilsWithDuration:(NSTimeInterval)aDuration afterDelay:(NSTimeInterval)aDelay;

/**
 * Return the current background image being shown
 *
 * @return the UIImage current background image
 */

- (UIImage *)getCurrentBackgroundImage;
    
```

###Code snippet

```objc
// First create a new view controller class that inherit from AOHomeViewController class and define the new controller conform to AOHomeViewController delegate protocol. Do not forget to import the AOHomeViewController interface

#import "AOHomeViewController.h"

@interface AOHomeController : AOHomeViewController <AOHomeViewControllerDelegate>

@end

// Then in the .m file define itself as the delegate

- (id)initWithNibName:(NSString *)nibNameOrNil bundle:(NSBundle *)nibBundleOrNil
{
    self = [super initWithNibName:nibNameOrNil bundle:nibBundleOrNil];
    if (self)
    {
        [self setDelegate:self];
    }
    return self;
}

// Then add medallion. One to create a new profile the other one to access existing profile.

- (void)viewWillAppear:(BOOL)animated
{
    [super viewWillAppear:animated];
    
    // Medallion to create new profile
    [self addMedallionWithImage:[UIImage imageNamed:@"defaultProfil"]
                       andTitle:NSLocalizedString(@"Add profile", @"")
                     newProfile:YES
                       userInfo:nil];
    
    // Medallion to access existing profile
    [self addMedallionWithImage:[UIImage imageNamed:@"tyrion.jpg"]
                       andTitle:@"Tyrion Lannister"
                     newProfile:NO
                       userInfo:@{@"image":[UIImage imageNamed:@"tyrion.jpg"], @"Name": @"Tyrion Lannister"}];
}

// Finally implement the delegate methods

- (void)newMedallionTapped
{
    NSLog(@"New profile touched up!");
}

- (void)medallionTappedWithUserInfo:(id)userInfo
{
    NSLog(@"Medallion profile touched up! > %@", userInfo);
}
```

Any comments are welcomed

@Appsido
contact@appsido.com

 [1]:http://public.appsido.com/iPhone/public/AOHome/AOHomeScreen_1.0.png
