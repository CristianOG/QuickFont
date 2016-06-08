QuickFont [![Join the chat at https://gitter.im/opcon/QuickFont](https://badges.gitter.im/opcon/QuickFont.svg)](https://gitter.im/opcon/QuickFont?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge) [![Build Status](https://travis-ci.org/opcon/QuickFont.svg?branch=master)](https://travis-ci.org/opcon/QuickFont) [![NuGet](https://img.shields.io/nuget/v/QuickFont.Desktop.svg?maxAge=2592000)](https://www.nuget.org/packages/QuickFont.Desktop/)
=========

A modern OpenGL text rendering library for OpenTK.

Forked from [swax/QuickFont](https://github.com/swax/QuickFont) library.
Original Library [QFont](http://www.opentk.com/project/QuickFont)

You can install this library via [nuget](https://www.nuget.org/packages/QuickFont.Desktop/).

## Supported Platforms

QuickFont has been tested and runs on Windows, Linux and OSX.

The minimum supported OpenGL version is 3.0

## Version 4.1
* Updated font loading mechanism to use [SharpFont](https://github.com/Robmaister/SharpFont) for loading fonts by path, and use the regular GDIFont mechanism for loading installed (system) fonts
* Updated example project to show some different installed system fonts

### Version 4.0
* Now uses SharpFont for loading the font files, so custom (non-installed) fonts are now supported on Linux and OSX
* Added Nuget package
* Added support for OpenGL ES (requires conditional compilation) thanks to [vescon](https://github.com/vescon/QuickFont)
* Improved Shader loading
* Cross-platform support (tested on Windows 10, Ubuntu 15.10, OSX 10.11,10.10)
* Unicode support
* Example is working again
* Updated to latest OpenTK nuget package (OpenTK.Next)

###Todo
- [ ] Maybe extract all Print methods in a static class to leave QFontDrawingPrimitive more basic.
- [ ] Right to Left text flow support (arabic, hebrew)
- [ ] Unicode zero spacing eg. combining character support
- [ ] On-the-fly character addition (If a character can not be found, add it, regenerate the font)

##Screenshot

![](https://i.imgur.com/lf0mKCl.png)

##Example

In some OnLoad() method create your QFont and your QFontDrawing
```C#
_myFont = new QFont("Fonts/HappySans.ttf", 72, new QFontBuilderConfiguration(true));
_myFont2 = new QFont("basics.qfont", new QFontBuilderConfiguration(true));
_drawing = new QFontDrawing();
```

Call some print methods or create Drawing primitives by themselves.
Add them to the drawing.
```C#
_drawing.DrawingPimitiveses.Clear();
_drawing.Print(_myFont, "text1", pos, FontAlignment.Left);

// draw with options
var textOpts = new QFontRenderOptions()
    {
	Colour = Color.FromArgb(new Color4(0.8f, 0.1f, 0.1f, 1.0f).ToArgb()),
	DropShadowActive = true
	};
SizeF size = _drawing.Print(_myFont, "text2", pos2, FontAlignment.Left, textOpts);

var dp = new QFontDrawingPimitive(_myFont2);
size = dp.Print(text, new Vector3(bounds.X, Height - yOffset, 0), new SizeF(maxWidth, float.MaxValue), alignment);
drawing.DrawingPimitiveses.Add(dp);

// after all changes do update buffer data and extend it's size if needed.
_drawing.RefreshBuffers();

```

Then in your draw loop do:
```C#
_drawing.ProjectionMatrix = proj;
_drawing.Draw();
SwapBuffers();
```

At the end of the program dispose the QuickFont resources:
```C#
protected virtual void Dispose(bool disposing)
{
	_drawing.Dispose();
	_myFont.Dispose();
	_myFont2.Dispose();
}
```

**See the included example project for more!**

## Contributors

The following is a non-exhaustive list of people who have contributed to QuickFont:

James Lohr - Creator of the original library (http://www.opentk.com/project/QuickFont)

John (swax) Marshall - Added vertex buffer support

Patrick (opcon) Yates - Current maintainer

Robertofon - Refactored monolithic QFont class

Martinay - OpenGL ES 2.0 support

Jan Polak

Jonathan

## License

Licensed under MIT, please see the file `License.txt` in the project root directory
