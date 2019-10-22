# Properties Stringifier
[![NuGet](https://img.shields.io/nuget/v/PropertiesStringifier.svg)](https://www.nuget.org/packages/PropertiesStringifier/)
#### A very simple and fast way to stringify your model class to help you while debugging.

When debugging, instead of seing this:
![Without Properties Stringifier](img/without-properties-stringifier.png?raw=true "Without Properties Stringifier")

You will see this:
![With Properties Stringifier](img/with-properties-stringifier.png?raw=true "With Properties Stringifier")

## Installation
Package Manager

`
Install-Package PropertiesStringifier
`

.NET CLI

`
dotnet add package PropertiesStringifier
`

## Basic Usage
Properties Stringifier comes in two flavors:

#### 1 - Overrides the "ToString()"
```csharp
using PropertiesStringifier;

public class Actress
{
    public string Name { get; set; }
    public int Age { get; set; }
    public DateTime BirthDate { get; set; }
    public bool IsDead { get; set; }

    // Will return "Name: Natalie Portman Age: 38 BirthDate: 1981-06-09 DeathDate: null IsDead: false"
    public override string ToString()
    {
        return this.StringifyProperties();
    }
}
```

#### 2 - Inherits from StringifyProperties base class
```csharp
using PropertiesStringifier;

public class Actress : StringifyProperties
{
    public string Name { get; set; }
    public int Age { get; set; }
    public DateTime BirthDate { get; set; }
    public bool IsDead { get; set; }
	
    // Method ToString() is already overrided in base class. Nothing to do here.
    // Will return "Name: Natalie Portman Age: 38 BirthDate: 1981-06-09 DeathDate: null IsDead: false"
}
```

## Advanced Usage with Fluent Style
You can specify the properties you want to stringify or the properties you want to ignore using the fluent-style methods.

#### Explicitly select the properties to stringify
```csharp
using PropertiesStringifier;

public class Actress
{
    public string Name { get; set; }
    public int Age { get; set; }
    public DateTime BirthDate { get; set; }
    public bool IsDead { get; set; }

    // Will return "Name: Natalie Portman Age: 38"
    public override string ToString()
    {
        return 
	    this
                .StringifyThisProperty(x => x.Name)
                .AndThisProperty(x => x.Age)
                .ToString();
    }
}
```

#### Chose properties to ignore
```csharp
using PropertiesStringifier;

public class Actress
{
    public string Name { get; set; }
    public int Age { get; set; }
    public DateTime BirthDate { get; set; }
    public bool IsDead { get; set; }

    // Will return "DeathDate: null LatestIntervewDatetime: 2019-05-18 12:15:16 MoviesCount: 5 NominationsCount: 3"
    public override string ToString()
    {
        return 
            this
                .StringifyPropertiesExcept(x => x.Name)
                .AndExceptThisProperty(x => x.Age)
                .AndExceptThisProperty(x => x.IsDead)
                .AndExceptThisProperty(x => x.BirthDate)
                .AndExceptThisProperty(x => x.MainMediaType)
                .ToString();
    }
}
```

That's all. 😊
