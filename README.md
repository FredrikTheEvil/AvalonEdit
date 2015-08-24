AvalonEdit XM
==========

Introduction
------------
AvalonEdit XM is a fork of AvalonEdit for implementing scope based syntax highlighting similar to TextMate/Sublime Text
The fork was created to facilitate easier coloring of syntax highlighting definitions, by using scopes to implement a scope stack for each span instead of a highlighting color.

Highlighting Engine
-------------------
The highlighting engine is the same as in AvalonEdit, but no tracking of HighlightingColor is done, instead scopes are tracked, and colorization uses scopes to look up a color in a theme. It uses the same scope matching rules as TextMate/Sublime Text for color lookup. 

Scopes
------
A scope can consist of multiple parts separated by '.' and it is matched against the most specific color found going right to left. Meaning if the current scope is 'variable.parameter.function.js' then it would match all of these colors, but it would use them in laid out order if all colors are present: variable.parameter.function.js, variable.parameter.function, variable.parameter
If only a color was set for variable, then that color would be used.

Motivation
----------
Creating fully themeable editors using AvalonEdit is currently alot of work. Named colors provide the ability to dynamically apply coloring to some degree, but it is limited by naming. You need to create a named color and thus support the name in your theme system. You may easily follow conventions while ensuring completeness in your themes, but this means more work for  theme authors. 

By using scopes which can be partially matched, and a guideline for scope naming conventions, it is possible to reuse the same colors for all syntax definitions. For AvalonEdit XM it is recommended to use the same naming conventions as used in TextMate/Sublime Text. Using conventions used in popular text editing software allows simple reuse of theming.
Conventions for TextMate can be found at https://manual.macromates.com/en/language_grammars

Future Additions
----------------
I want to make the syntax highlighting component more abstract and allow it to be replaced as easily as replacing syntax definitions. This is because I want to be able to use definition based syntax higlighting, as well as using code based highlighting, implemented by analyzing code syntax trees from the text, like using the Roslyn API for C# and VB .NET highlighting.

Import of syntax definitions from TextMate/Sublime Text. This is easily done, but because of differences in the Regular Expressions engine used in TextMate/Sublime vs .NET, the imported languages might not work properly if more exotic features are used. It's possible to create a regex transformer for these edge cases, but I may not bother with the extra work. It's a low priority
