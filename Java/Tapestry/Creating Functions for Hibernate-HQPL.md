In myproject i was using multiple Join in my code in order to get a selection that it was required.
In order to simplify the code dramatically a function needed to be created.

My model consisted of the following 
```
@Getter
@Setter
@NoArgsConstructor
@Entity
@Table(name = "our_table_name")
public class OurTableName extends HibernateObject
```

The Getter/Setters and Constructor are generated automatically with Lombok.
This removed a lot of the boilerplate of each model.
The HibernateObject is simply an class that hold in my primary key for all my model.

In my DAO i had my HibernateQuery that would create multiple JPQLSubQuery and several more Expressions.
What was required was in our DAO object, or where ever you want, was to get the currentSession first
```
org.hibernate.sessionFactory.getCurrentSession();
```

And then create our Name Query where we defind the name of the query and we can pass in any variable we want to our function.

```
Query q = getCurrentSession().getNamedQuery("thisIsACustomFunction")
			.setInteger("objectIntger",valueInt)
			.setDate("objectDate",valueDate); // or setTime or setTimestamp
```

Our Function is coupled with a model as it will return a set of the object that we require.
A function will look something like this and return the row from our table.
```
CREATE OR REPLACE FUNCTION this_is_a_custom_function (IN firstValue integer, IN secondValue date)
 RETURNS SETOF our_table_name AS $$
  SELECT * FROM our_table_name;
 $$ LANGUAGE SQL;
```

As this needs to return an instance of the model that we want to use we need to combine it with the model that we created before.

```
@NamedNativeQuery(
	name = "thisIsACustomFunction", 
	query = "SELECT * FROM this_is_a_custom_function(:objectIntger,:objectDate)",
	resultClass = OurTableName.class)
@Getter
@Setter
@NoArgsConstructor
@Entity
@Table(name = "our_table_name")
public class OurTableName extends HibernateObject {
```

By creating our @NamedNativeQuery we are immediately coupling the values of our query to our model.

