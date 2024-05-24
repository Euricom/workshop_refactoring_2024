---
theme: euricom
lineNumbers: true
hideInToc: true
layout: cover
background: /zen-stones-sand-background-health-wellness-concept.jpg
---

# Workshop Refactoring

## Improving the design of existing code

> Euricom - 2024

---<!-- prettier-ignore -->
layout: quote
author: Martin Fowler
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg

---

<style>
  p {
    @apply text-black text-2xl
  }
  
</style>

Refactoring is the process of changing a software system in a way that does not alter the external behavior of the code yet improves its internal structure.

---<!-- prettier-ignore -->
layout: quote
author: Martin Fowler
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg

---

<style>
  p {
    @apply text-black text-2xl
  }
  
</style>

Any fool can write code that a computer can understand. Good programmers write code that humans can understand.

---<!-- prettier-ignore -->
layout: cover
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg

---

# Primitive obsession

Primitive obsession is a code smell, look at the following code snippet:

```cs

public void RegisterUser(string email, string rijksregisterNummer)

```

<v-click> 

Better

```cs

public void RegisterUser(Email email, RijksregisterNummer rijksregisterNummer)

```
</v-click>

<!-- 
- What if someone changes the order of the parameters?
- Are the values already validated or should I do it (again)
- How are the values formatted?
 -->

---<!-- prettier-ignore -->
layout: cover
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg
---

# Example implementation

```cs

public record struct RijksregisterNummer
{
    public string Value { get; }

    public RijksregisterNummer(string value)
    {
        // Validate number here
        // Format number here
        Value = value;
    }

    public static RijksregisterNummer Empty { get; } = new("00.00.00-000-00");
}
```

---<!-- prettier-ignore -->
layout: cover
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg

---

# Example implementation

```cs

public static RijksregisterNummer Parse(string value)
{
    if (IsValid(value))
        return new RijksregisterNummer(value);

    throw new ArgumentException("Ongeldig rijksregister nummer");
}

public static bool TryParse(string value, out RijksregisterNummer rijksregisterNummer)
{
    var isValid = IsValid(value);
    rijksregisterNummer = isValid ? new RijksregisterNummer(value) : Empty;
    return isValid;
}

```

---<!-- prettier-ignore -->
layout: cover
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg

---

# Example implementation

```cs

public override string ToString()
{
    return _value;
}

public static implicit operator string(RijksregisterNummer rijksregisterNummer)
{
    return rijksregisterNummer._value;
}

```

---<!-- prettier-ignore -->
layout: cover
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg

---

# Enum Pattern

---<!-- prettier-ignore -->
layout: cover
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg

---

# Refactoring Rules

<v-clicks>

- work in small teams (max 3)
- treat fellow team members with kindness and respect.
- follow the driver-navigator approach.
- failing is ok
- small steps, you don't want to break the code

</v-clicks>

---<!-- prettier-ignore -->
layout: cover
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg

---

# Gilded Rose 🌹

https://github.com/emilybache/GildedRose-Refactoring-Kata

<v-clicks>

- je bent een nieuwe aanwinst in het team
- het bedrijf verkoopt de beste goederen
- enige nadeel is dat ze kwaliteit verliezen hoe ouder ze worden
- je eerste user story is het toevoegen van een nieuw artikel "Conjured", die 2 maal zo snel hun kwaliteit verliezen
- je mag alleen maar wijzigingen aanbrengen aan de updateQuality methode, de rest moet hetzelfde blijven, daar heel het platform rekent op de code
- kijk niet naar requirements!

</v-clicks>

---<!-- prettier-ignore -->
layout: cover
background: /lukas-blazek-EWDvHNNfUmQ-unsplash.jpg

---

# Tennis Game 🎾

https://github.com/emilybache/Tennis-Refactoring-Kata

<v-clicks>

- je bent een software consultant
- een collega van je is ziek geworden, er rest nog 1,5u van de 10 voorziene uren
- je opdracht is om de code wat te verbeteren en op te kuisen

</v-clicks>
