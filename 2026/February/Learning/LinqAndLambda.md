# LINQ Fundamentals in C#

## 1. Introduction

LINQ (Language Integrated Query) allows querying and transforming data collections using C# syntax.  
It works with:

- In-memory collections (List<T>, arrays)
- Databases (via Entity Framework / IQueryable)
- XML
- Any IEnumerable<T> source

LINQ promotes:
- Declarative style
- Readable transformations
- Reduced boilerplate code
- Functional programming concepts

---

## 2. IEnumerable<T> — The Foundation

Most LINQ methods operate on IEnumerable<T>.

Example:

```csharp
string name = "Sarada";

foreach (char c in name)
{
    Console.WriteLine(c);
}
```
A string implements IEnumerable<char>, so LINQ works on it directly.

## 3. Core LINQ Methods
### 3.1 Where() — Filtering
Filters elements based on a condition.

var result = numbers.Where(n => n > 5);
### 3.2 Select() — Projection
Transforms each element into a new form.

var result = numbers.Select(n => n * 2);
### 3.3 OrderBy() and OrderByDescending()
Sorts elements.

var result = numbers.OrderBy(n => n);
var resultDesc = numbers.OrderByDescending(n => n);
To apply multiple sorting conditions:

var result = numbers
    .OrderBy(n => n)
    .ThenBy(n => n);
Important:

OrderBy starts a new sorting.

ThenBy continues existing sorting.

Calling OrderBy again resets previous sorting.

### 3.4 Distinct()
Removes duplicate values.

var unique = names.Distinct();
Case-insensitive distinct:

var unique = names.Distinct(StringComparer.OrdinalIgnoreCase);
### 3.5 GroupBy()
Groups elements by a key.

var grouped = names.GroupBy(n => n.Length);

foreach (var group in grouped)
{
    Console.WriteLine($"Length: {group.Key}");
    foreach (var item in group)
        Console.WriteLine(item);
}
## 4. Deferred vs Immediate Execution
Deferred Execution
These methods do not execute immediately:

Where

Select

OrderBy

GroupBy

Execution happens when you iterate or call a terminal method.

Example:

var query = numbers.Where(n => n > 2); // not executed yet
Execution happens when:

var list = query.ToList();
Immediate Execution
These trigger execution:

ToList()

ToArray()

Count()

First()

Sum()

## 5. Practical Example
List<string> names = new List<string>
{
    "Sarada",
    "Ranjan",
    "Behera",
    "Sam",
    "Rita",
    "Sarada",
};

var SName = names
    .Where(name => name.StartsWith("S"))
    .Select(name => name.ToUpper())
    .OrderByDescending(name => name)
    .ToList();

Console.WriteLine(string.Join(", ", SName));

var SName2 = names
    .Where(name => name.StartsWith("S", StringComparison.OrdinalIgnoreCase)
                || name.StartsWith("R", StringComparison.OrdinalIgnoreCase))
    .Distinct(StringComparer.OrdinalIgnoreCase)
    .OrderByDescending(name => name.Length)
    .ThenBy(name => name)
    .ToList();

Console.WriteLine(string.Join(", ", SName2));
## 6. Explanation of Example
First Query
.Where(name => name.StartsWith("S"))
Filters names starting with "S" (case-sensitive).

.Select(name => name.ToUpper())
Converts results to uppercase.

.OrderByDescending(name => name)
Sorts alphabetically descending.

Result:
SARADA, SARADA, SAM

Note:
Duplicates remain because Distinct() was not used.

Second Query
.Where(...)
Filters names starting with S or R (case-insensitive).

.Distinct(StringComparer.OrdinalIgnoreCase)
Removes duplicates ignoring case.

.OrderByDescending(name => name.Length)
.ThenBy(name => name)
Primary sort: length descending
Secondary sort: alphabetical ascending

Result:
Sarada, Ranjan, Rita, Sam

## 7. Performance Considerations
Prefer comparer-based logic over transforming data unnecessarily.
Example:
Distinct(StringComparer.OrdinalIgnoreCase)
is more efficient than
Select(n => n.ToUpper()).Distinct()

Avoid calling ToList() too early.
Keep query deferred as long as possible.

In Entity Framework:

IQueryable translates to SQL.

Calling ToList() forces in-memory evaluation.

## 8. IEnumerable vs IQueryable
IEnumerable<T>

Works in memory

Uses delegates

Executes locally

IQueryable<T>

Builds expression trees

Translates to SQL

Executes in database

Important:
Calling ToList() converts IQueryable into IEnumerable.

## 9. Key Takeaways
LINQ is about querying, not storing data.

Understand deferred execution.

Use ThenBy for multi-level sorting.

Use comparers instead of transforming data when possible.

Know the difference between IEnumerable and IQueryable.

Order of operations in LINQ matters.

End of Tutorial


---

If you want next, I can prepare:

- Advanced LINQ (Join, SelectMany, GroupJoin)
- LINQ interview questions
- LINQ performance deep dive
- LINQ vs SQL comparison for architects

Tell me which direction you want.
