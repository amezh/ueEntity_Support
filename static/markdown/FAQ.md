# FAQ
---

## What Entity framework is under the hood?

ENTT by skypjack https://github.com/skypjack/entt

---

## Do I need Engine source code to build the plugin?

Nope

---

##  Does it work on the mobile platform of my choice?

Yes

---

## What are prerequisites to make it work?

None, install the plugin and you're good to go.

---

## I'm getting intelisense\build errors in hpp files

Yeah, that's an unfortunate inconvenience. Visual Studio doesn't know that your compiler is using cpp17, so highlights those as errors.
Ignore those errors for now and check your output log for the real issue.

---

## Blueprint nativization doesn't work

Correct! Plugin it generates doesn't use cpp17, but fear not!
Navigate to your engine folder like UE_4.23\Engine\Content\Editor\Templates  find PluginModule.Build.cs.template (make a backup if you want)

Modify it to look like so and you're good to go:

```C#
PCHUsage = PCHUsageMode.NoSharedPCHs;
PrivatePCHHeaderFile = "Private/%MODULE_NAME%.h";
CppStandard = CppStandardVersion.Cpp17;
bLegacyPublicIncludePaths = Target.bLegacyPublicIncludePaths;
```

---

## I'm getting an error about /std:cpp17

modify your project .Build.cs file to have:

```C#
PCHUsage = PCHUsageMode.NoSharedPCHs;
CppStandard = CppStandardVersion.Cpp17;
PrivatePCHHeaderFile = "<you project name>.pch.h";
```

---

## Do I need to know C++ to use the plugin?

I would recommend it, but no.

---

## Is it thread-safe?

Yes and no. Everything in core functionality can be attached-detached from any thread, however, there is no safety ensuring mechanisms 

---