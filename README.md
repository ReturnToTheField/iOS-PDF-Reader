# iOS-PDF-Reader
PDF Reader for iOS written in Swift

## Installation

[CocoaPods]: http://cocoapods.org

To install it, simply add the following line to your **Podfile**:

```ruby
pod 'PDFReader', :git => 'https://github.com/Alua-Kinzhebayeva/iOS-PDF-Reader.git'
```

You will also need to make sure you're opting into using frameworks:

```ruby
use_frameworks!
```

Then run `pod install` with CocoaPods 1.0 or newer.

## Usage

### Option 1: Instantiate a PDFViewController and manually push it to an existing navigation controller
```swift
dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0)) {
    let pdfDocument = PDFDocument(tempURL: pdfURL)
    dispatch_async(dispatch_get_main_queue()) {
        let storyboard = UIStoryboard(name: "PDFReader", bundle: NSBundle(forClass: PDFViewController.self))
        let controller = storyboard.instantiateInitialViewController() as! PDFViewController
        controller.document = pdfDocument
        controller.title = "Document"
        self.navigationController?.pushViewController(controller, animated: true)
    }
}
```

### Option 2: Create a [Storyboard Referenece](https://developer.apple.com/library/ios/recipes/xcode_help-IB_storyboard/Chapters/AddSBReference.html) in an existing storyboard and present the PDFViewController
```swift
dispatch_async(dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0)) {
    self.pdfDocument = PDFDocument(tempURL: pdfURL)
    dispatch_async(dispatch_get_main_queue()) {
        self.performSegueWithIdentifier("presentPDFReader", sender: pdfDocument)
    }
}

...

override func prepareForSegue(segue: UIStoryboardSegue, sender: AnyObject?) {
    if let controller = segue.destinationViewController as? PDFViewController {
        controller.document = self.pdfDocument
        controller.title = "Document"
    }
}
```
# TODO
- Displaying two pages in landscape orientation

# Acknowledgements

inspired by PDF Reader https://github.com/vfr/Reader and Apple's example on TiledScrollView