
# OuterRef

Assuming we have models Parent and Child, and Child has a foreign key to Parent

```
parents_query = Parent.objects.all()

children_subquery = Child.objects.filter(
    parent_id=OuterRef('pk'),
    name__startswith='A'
)
```

In a way, doing this is similar to the following as they serve the same purpose. 

```
children_subquery = Child.objects.filter(
    parent__in=parents_query
    name__startswith='A'
)
```

#### parent_id=OuterRef('pk'): 
-> Dynamic.

-> It's like creating a placeholder that says, "Insert the primary key from the outer query here."

#### parent__in=parents_query
-> Static.

-> You first execute parents_query to get the list of IDs, and then you use these IDs to filter another query.

