[![Platform](https://img.shields.io/cocoapods/p/TGLStackedViewController.svg?maxAge=86400)](http://cocoadocs.org/docsets/TGLStackedViewController)
[![Tag](https://img.shields.io/github/tag/gleue/TGLStackedViewController.svg?maxAge=86400)](https://github.com/gleue/TGLStackedViewController/tags)
[![CocoaPods](https://img.shields.io/badge/CocoaPods-compatible-4BC51D.svg?style=flat)](https://cocoapods.org)
[![Carthage](https://img.shields.io/badge/Carthage-compatible-4BC51D.svg?style=flat)](https://github.com/Carthage/Carthage)
[![License](https://img.shields.io/github/license/gleue/TGLStackedViewController.svg?maxAge=86400)](https://opensource.org/licenses/MIT)
[![Downloads](https://img.shields.io/cocoapods/dt/TGLStackedViewController.svg?maxAge=86400)](https://cocoapods.org/pods/TGLStackedViewController)

TGLStackedViewController
========================

A stack layout with gesture-based reordering using UICollectionView -- inspired by Passbook and Reminders apps.

What's new in 2.2
------------------

* Reimplementation of item reordering using UIKit drag and drop on iOS 11.0

What's new in 2.0
------------------

* Uses iOS 9 collection view reordering API instead of own implementation, therefore minimum deployment target is iOS 9.0
* Unexposed items are pinned to bottom by default, now 
* The exposed item can be collapsed interactively in addition to tapping it
    * When pinning (the default) pan item down to switch back to stacked layout
    * When just pushing cards aside use pinch gesture instead
* Improved sample project w/ lots of settings to tweak interactively

<p align="center">
<img src="https://raw.github.com/gleue/TGLStackedViewController/master/Screenshots/TGLStackedViewExample.gif" alt="TGLStackedViewExample" title="TGLStackedViewExample">
</p>

Getting Started
===============

Take a look at sample project `TGLStackedViewExample.xcodeproj`. You may use sample class `TGLViewController` as a starting point for your own implementation. 

Usage
=====

Via [CocoaPods](http://cocoapods.org):

* Add `pod 'TGLStackedViewController', '~> 2.2'`  to your project's `Podfile`

Via [Carthage](https://github.com/Carthage/Carthage):

* Add `github "gleue/TGLStackedViewController", ~> 2.2`  to your project's `Cartfile`

Or the "classic" way:

* Add files in folder `TGLStackedViewController` to your project

Then in your project:

* Create a subclass derived from `TGLStackedViewController`
* Implement the `UICollectionViewDataSource` protocol in your subclass
    * *Currently only 1 section is supported* therefore your implementation of `-numberOfSectionsInCollectionView` *has to* return `1`. `TGLStackedViewController` provides a suitable implementation for you -- no need to overwrite.
    * Implement methods `-numberOfSectionsInCollectionView:` and `-collectionView:cellForItemAtIndexPath` as usual.
    * **New in 2.0**: `TGLStackedViewController`'s implementation of method `-collectionView:canMoveItemAtIndexPath:` checks for stacked layout and a minimum number of 2 items before allowing reordering. Make sure to call `super` in your implementation and honor it's result.
    * **New in 2.0**: Implement method `-collectionView:moveItemAtIndexPath:toIndexPath:` to update your data model after items have been reordered
* Implement the `UICollectionViewDelegate` protocol in your subclass
    * `TGLStackedViewController` already implements methods `-collectionView:shouldHighlightItemAtIndexPath:`, `-collectionView:didDeselectItemAtIndexPath`, and `-collectionView:didSelectItemAtIndexPath:` internally, so make sure to call `super` in your implementation.
    * Method `-collectionView:targetContentOffsetForProposedContentOffset:` is crucuial for properly transitioning betwenn exposed and stacked layout, so make sure to call `super` in your implementation.
* Place `UICollectionViewController` in your storyboard and set its class to your derived class
    * Make sure to set up the collection view's `delegate` and `dataSource` connections properly
* **New in 2.0**: `TGLStackedViewController` does no longer create a layout object internally.
    * Set the collection view controller's layout class to `TGLStackedLayout` or your own subclass of `TGLStackedLayout` in the inspector in Interface Builder.
    * When creating a `TGLStackedViewController` in code you have to set the collection view's layout before presenting the view controller.

Requirements
============

* ARC
* iOS >= 9.0
* Xcode 9.0

Credits
=======

- Reordering in 1.x based on [LXReorderableCollectionViewFlowLayout](https://github.com/lxcid/LXReorderableCollectionViewFlowLayout)
- Original `Podspec` by [Pierre Dulac](https://github.com/dulaccc)
- Carthage support by [Hannes Oud](https://github.com/hannesoid)

License
=======

TGLStackedViewController is available under the MIT License (MIT)

Copyright (c) 2014-2019 Tim Gleue (http://gleue-interactive.com)

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
