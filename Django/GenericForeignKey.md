# GenericForeignKey

Basically, it is a foreign key that can point to any model.
It is a combination of = Object_id + content_type.

- Django uses a `ContentType` model to keep track of all models in the application. Each model is identified uniquely by its `app_label` and `model name`


### Tagging System

```
class TaggedItem(models.Model):
   
    content_type = models.ForeignKey(ContentType, on_delete=models.CASCADE)
    object_id = models.PositiveIntegerField()
    content_object = GenericForeignKey('content_type', 'object_id')

    tag = models.CharField(max_length=255)

```
Now you can create tags for models like `Article` and `Product` as follows:


from django.contrib.contenttypes.models import ContentType

```
article = Article.objects.get(id=1)
product = Product.objects.get(id=1)

# Creating tags
article_tag = TaggedItem(content_object=article, tag='Interesting')
article_tag.save()

product_tag = TaggedItem(content_object=product, tag='On Sale')
product_tag.save()
```
