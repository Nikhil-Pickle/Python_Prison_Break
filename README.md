# Analyzing Data

## Prison Helicopter Escapes

We begin by importing some helper functions.


```python
from helper import *
```

## Get the Data

Now, let's get the data from the [List of helicopter prison escapes](https://en.wikipedia.org/wiki/List_of_helicopter_prison_escapes) Wikipedia article.


```python
url = 'https://en.wikipedia.org/wiki/List_of_helicopter_prison_escapes'
```


```python
data = data_from_url(url)
```

Let's print the first three rows.


```python
for row in data[:3]:
    print(row)
```

    ['August 19, 1971', 'Santa Martha Acatitla', 'Mexico', 'Yes', 'Joel David Kaplan Carlos Antonio Contreras Castro', "Joel David Kaplan was a New York businessman who had been arrested for murder in 1962 in Mexico City and was incarcerated at the Santa Martha Acatitla prison in the Iztapalapa borough of Mexico City. Joel's sister, Judy Kaplan, arranged the means to help Kaplan escape, and on August 19, 1971, a helicopter landed in the prison yard. The guards mistakenly thought this was an official visit. In two minutes, Kaplan and his cellmate Carlos Antonio Contreras, a Venezuelan counterfeiter, were able to board the craft and were piloted away, before any shots were fired.[9] Both men were flown to Texas and then different planes flew Kaplan to California and Contreras to Guatemala.[3] The Mexican government never initiated extradition proceedings against Kaplan.[9] The escape is told in a book, The 10-Second Jailbreak: The Helicopter Escape of Joel David Kaplan.[4] It also inspired the 1975 action movie Breakout, which starred Charles Bronson and Robert Duvall.[9]"]
    ['October 31, 1973', 'Mountjoy Jail', 'Ireland', 'Yes', "JB O'Hagan Seamus TwomeyKevin Mallon", 'On October 31, 1973, an IRA member hijacked a helicopter and forced the pilot to land in the exercise yard of Dublin\'s Mountjoy Jail\'s D Wing at 3:40\xa0p.m., October 31, 1973. Three members of the IRA were able to escape: JB O\'Hagan, Seamus Twomey and Kevin Mallon. Another prisoner who also was in the prison was quoted as saying, "One shamefaced screw apologised to the governor and said he thought it was the new Minister for Defence (Paddy Donegan) arriving. I told him it was our Minister of Defence leaving." The Mountjoy helicopter escape became Republican lore and was immortalized by "The Helicopter Song", which contains the lines "It\'s up like a bird and over the city. There\'s three men a\'missing I heard the warder say".[1]']
    ['May 24, 1978', 'United States Penitentiary, Marion', 'United States', 'No', 'Garrett Brock TrapnellMartin Joseph McNallyJames Kenneth Johnson', "43-year-old Barbara Ann Oswald hijacked a Saint Louis-based charter helicopter and forced the pilot to land in the yard at USP Marion. While landing the aircraft, the pilot, Allen Barklage, who was a Vietnam War veteran, struggled with Oswald and managed to wrestle the gun away from her. Barklage then shot and killed Oswald, thwarting the escape.[10] A few months later Oswald's daughter hijacked TWA Flight 541 in an effort to free Trapnell."]



```python
index = 0
for row in data:
    data[index] = row[:-1]
    index += 1
```


```python
print(data[:3])
```

    [['August 19, 1971', 'Santa Martha Acatitla', 'Mexico', 'Yes', 'Joel David Kaplan Carlos Antonio Contreras Castro'], ['October 31, 1973', 'Mountjoy Jail', 'Ireland', 'Yes', "JB O'Hagan Seamus TwomeyKevin Mallon"], ['May 24, 1978', 'United States Penitentiary, Marion', 'United States', 'No', 'Garrett Brock TrapnellMartin Joseph McNallyJames Kenneth Johnson']]



```python
for row in data:
    year = fetch_year(row[0])
    row[0] = year
```


```python
print(data[:3])
```

    [[1971, 'Santa Martha Acatitla', 'Mexico', 'Yes', 'Joel David Kaplan Carlos Antonio Contreras Castro'], [1973, 'Mountjoy Jail', 'Ireland', 'Yes', "JB O'Hagan Seamus TwomeyKevin Mallon"], [1978, 'United States Penitentiary, Marion', 'United States', 'No', 'Garrett Brock TrapnellMartin Joseph McNallyJames Kenneth Johnson']]



```python
min_year = min(data, key=lambda x: x[0])[0]
max_year = max(data, key=lambda x: x[0])[0]
```


```python
print(min_year)
print(max_year)
```

    1971
    2020



```python
years = []
for year in range(min_year, max_year + 1):
    years.append(year)
```


```python
print(years)
```

    [1971, 1972, 1973, 1974, 1975, 1976, 1977, 1978, 1979, 1980, 1981, 1982, 1983, 1984, 1985, 1986, 1987, 1988, 1989, 1990, 1991, 1992, 1993, 1994, 1995, 1996, 1997, 1998, 1999, 2000, 2001, 2002, 2003, 2004, 2005, 2006, 2007, 2008, 2009, 2010, 2011, 2012, 2013, 2014, 2015, 2016, 2017, 2018, 2019, 2020]



```python
attempts_per_year = []
for year in years:
    attempts_per_year.append([year, 0])
```


```python
print(attempts_per_year)
```

    [[1971, 0], [1972, 0], [1973, 0], [1974, 0], [1975, 0], [1976, 0], [1977, 0], [1978, 0], [1979, 0], [1980, 0], [1981, 0], [1982, 0], [1983, 0], [1984, 0], [1985, 0], [1986, 0], [1987, 0], [1988, 0], [1989, 0], [1990, 0], [1991, 0], [1992, 0], [1993, 0], [1994, 0], [1995, 0], [1996, 0], [1997, 0], [1998, 0], [1999, 0], [2000, 0], [2001, 0], [2002, 0], [2003, 0], [2004, 0], [2005, 0], [2006, 0], [2007, 0], [2008, 0], [2009, 0], [2010, 0], [2011, 0], [2012, 0], [2013, 0], [2014, 0], [2015, 0], [2016, 0], [2017, 0], [2018, 0], [2019, 0], [2020, 0]]



```python
for row in data:
    for year_attempt in attempts_per_year:
        year = year_attempt[0]
        if row[0] == year:
            year_attempt[1] += 1

print(attempts_per_year)
```

    [[1971, 1], [1972, 0], [1973, 1], [1974, 0], [1975, 0], [1976, 0], [1977, 0], [1978, 1], [1979, 0], [1980, 0], [1981, 2], [1982, 0], [1983, 1], [1984, 0], [1985, 2], [1986, 3], [1987, 1], [1988, 1], [1989, 2], [1990, 1], [1991, 1], [1992, 2], [1993, 1], [1994, 0], [1995, 0], [1996, 1], [1997, 1], [1998, 0], [1999, 1], [2000, 2], [2001, 3], [2002, 2], [2003, 1], [2004, 0], [2005, 2], [2006, 1], [2007, 3], [2008, 0], [2009, 3], [2010, 1], [2011, 0], [2012, 1], [2013, 2], [2014, 1], [2015, 0], [2016, 1], [2017, 0], [2018, 1], [2019, 0], [2020, 1]]


## Visualize the data


```python
%matplotlib inline
barplot(attempts_per_year)
```


    
![png](output_22_0.png)
    


2009, 2007, 2001, 1986 were the years with the most plane crashes of which was 3 plane crashes each year

And now for the best part:
instead of writing out all the code I wrote under the "Get the Data" section, I can use 1 line of code below to get it all done!


```python
countries_frequency = df["Country"].value_counts()
```


```python
print_pretty_table(countries_frequency)
```


<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>Country</th>
      <th>Number of Occurrences</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>France</td>
      <td>15</td>
    </tr>
    <tr>
      <td>United States</td>
      <td>8</td>
    </tr>
    <tr>
      <td>Belgium</td>
      <td>4</td>
    </tr>
    <tr>
      <td>Greece</td>
      <td>4</td>
    </tr>
    <tr>
      <td>Canada</td>
      <td>4</td>
    </tr>
    <tr>
      <td>United Kingdom</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Brazil</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Australia</td>
      <td>2</td>
    </tr>
    <tr>
      <td>Netherlands</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Puerto Rico</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Mexico</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Russia</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Ireland</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Chile</td>
      <td>1</td>
    </tr>
    <tr>
      <td>Italy</td>
      <td>1</td>
    </tr>
  </tbody>
</table>


far less coding required!
