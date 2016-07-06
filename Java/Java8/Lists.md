#### Sorting Lists ####

```
List<Company> companies = new ArrayList<>();

companies.add(new Company("Company A"));
companies.add(new Company("Company D"));
companies.add(new Company("Company C"));
companies.add(new Company("Company D"));
```


On Java 7 Sorting was done from the Collection passing a comparator
```
Collections.sort(companies, new Comparator<Company>(){
  public int compare(Company c1, Company c2){
    return c1.getName().compareTo(c2.getName());
  }
});
```


Using Lambda Expressions and Collection 
```
Collections.sort(companies, (Company c1, Company c2) -> c1.getName().compareTo(c2.getName()));
```


We can also remove the type information as it is redundat
```
Collections.sort(companies, (c1, c2) -> c1.getName().compareTo(c2.getName()));
```



And also we can use the sort method of the list
```
companies.sort((c1, 2 -> c1.getName().compareTo(c2.getName()));
```
