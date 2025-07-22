# QuickSuite
> Move Fast, but Correctly.

This repo contains some info, for me mostly, about the various Quick... libs I have lying around.

## Top Todo's
- [x] QuickAcid: Finish and check the Report to CaseFile refactoring
- [ ] QuickAcid: Publish

## Active Projects

## [QuickAcid](https://github.com/kilfour/QuickAcid)
> Drop it in acid. Look for gold. Like alchemy, but reproducible.

PBT framework. Main focus, most other projects support this one.

### Depends On  
 - QuickFuzzr
 - QuickPulse
 - QuickPulse.Show

### Tests Depend On 
 - QuickPulse.Explains

### Todo
- [x] Migrate to QuickPulse.Explains
- [ ] Lots

This is the core, the Linqy bit, there's a variety of experiments in different projects, notably:

#### QuickAcid.Fluent
Fluent interface for easier onboarding, less power, harder to shoot yourself in the face.

#### QuickAcid.Refinery
A working spike and some tests. Generates [Fact]'s from the QuickAcid report.

**TODO:** use the new casefile instead of the report and it should work for even the hard tests.

## [QuickFuzzr](https://github.com/kilfour/QuickFuzzr)
> A type-walking cheetah with a hand full of random.

Very stable, first lib using the auto doc system.
Used to supply fuzzers for QuickAcid mainly these days.

### Tests Depend On 
 - QuickPulse
 - QuickAcid

### Todo
- [ ] Overload `.Unique()` with `() => ""` in order to set dynamic keys for unique checks
- [ ] Check and document one to many default generation
- [ ] Use QuickPulse.Explains
- [ ] Split Docs into different files.

## [QuickPulse](https://github.com/kilfour/QuickPulse) 
> LINQ with a heartbeat.

Delightfull little lib I never knew I needed, ... but I do.
Flow based execution. A portable state machine. Used in a lot of other projects.

### Tests Depend On 
 - QuickPulse.Explains

### Todo
- [x] Migrate to QuickPulse.Explains
- [x] Split Docs into different files.
- [ ] Doc the flow factory overloads.
- [ ] Doc the Valve.
- [ ] Doc the small sugaring methods.

## [QuickPulse.Show](https://github.com/kilfour/QuickPulse.Show)
> Please allow `this` to introduce oneself, hope you guess my type.

Does one thing, but does it well.
```csharp
Introduce.This(new List<Person> { new("Alice", 26), new("Bob", 21) }, false);
    // => "[ { Name: \"Alice\", Age: 26 }, { Name: \"Bob\", Age: 21 } ]"
```
### Depends On 
 - QuickPulse

### Tests Depend On 
 - QuickFuzzr
 - QuickPulse.Explains

### Todo
- [x] Use QuickPulse.Explains.
- [ ] Doc customization.

## [QuickPulse.Explains](https://github.com/kilfour/QuickPulse.Explains)
> Write some tests, make QuickPulse read them aloud.

The home of the auto doc system.

### Depends On  
 - QuickPulse

## Quick but Old

## QuickExplainIt (OBSOLETE)
Superseded by QuickPulse.Explains, basically a rename.

### QuickMGenerate (OBSOLETE)
Superseded by QuickFuzzr, basically a rename.

Also `Fuzz.Int()` much better than `MGen.Int()`.

### QuickGenerate (OBSOLETE)
The original Generator lib. Fluent style, obsolete, superseded by QuickMGenerate.
Does contain some test patterns which I might move to an active project.

### QuickXml 
Linqy Xml Parser, not bad, not great. No commits in over 7 years.
```csharp
[Fact]
public void ReadingTwoNodes()
{
    const string input = "<root><first>a first</first><second>a second</second></root>";

    var xmlParser =
        from first in XmlParse.Child("first").Content()
        from second in XmlParse.Child("second").Content()
        select new[] { first, second };

    var result = xmlParser.Parse(input);
    Assert.Equal("a first", result[0]);
    Assert.Equal("a second", result[1]);
}
```

### QuickXmlWrite 
The opposite of QuickXml, not bad, not great. No commits in over 7 years.
```csharp
[Fact]
public void WritingAnObject()
{
    var writer =
        from root in XmlWrite.For<MyThing>().Tag("root")
        from myStringContent in root.Tag("string").Content(x => x.MyString)
        from myIntContent in root.Tag("int").Content(x => x.MyInt.ToString())
        select root;
    var expected = "<root><string>some text</string><int>42</int></root>";

    var thing = new MyThing { MyString = "some text", MyInt = 42 };
    var actual = writer.Write(thing);
    Assert.Equal(expected, actual);
}
```

### QuickInspect
A graph traversing MemberwiseEqual mainly, no commits in 7 years.
Could be rewritten, might be useful.

### QuickDotNetCheck (OBSOLETE)
The OG testing lib i wrote a long time ago. Superseded by QuickAcid, no commits in over 10 years. 
A dead artifact preserved for history. Interesting take though.


