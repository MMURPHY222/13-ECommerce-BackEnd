# 13-ECommerce-BackEnd

## User Story

```md
AS A manager at an internet retail company
I WANT a back end for my e-commerce website that uses the latest technologies
SO THAT my company can compete with other e-commerce companies
```

## Link to video
https://drive.google.com/file/d/15zxjCCChkSVvc3sVC1nd-CHRCK1uuoFv/view

## Functionality
```md
This project was to finalize functionality of get, post, and delete requests on the back end of the application. Models also needed to be created, along with pathing and index.js files within the model and routes folder. 
```

```md
All of the get routes looked pretty similar they were written as async await promises with try catch blocks within. Here is an example of the get all request for the categories, notice with the include they wanted to products within each category to also be shown. 
```

```javascript
router.get('/', async (req, res) => {
  // find all categories
  // be sure to include its associated Products
  try {
    const categoryData = await Category.findAll({
      include: [{model: Product}]
    });
    res.status(200).json(categoryData);
  } catch (err) {
    res.status(500).json(err);
  }
});
```

```md
Post request were also pretty similar across all routes. They used req.body to access the information inside the request and created a new object and posted that to the database. Here is an example from the categories route. 
```

```javascript
router.post('/', async (req, res) => {
  // create a new category
  let newCat = {
    category_name: req.body.category_name,
  }
  console.log(req.body);
  try {
    const categoryData = await Category.create(newCat);
    res.status(200).json(categoryData);
  } catch (err) {
    res.status(400).json(err);
  }
});
```

```md
Similarly with post routes they used the sequelize update clause and were identified by the id of the object that was requested for update. Here is an example from the categories route. 
```

```javascript
router.post('/', async (req, res) => {
  // create a new category
  let newCat = {
    category_name: req.body.category_name,
  }
  console.log(req.body);
  try {
    const categoryData = await Category.create(newCat);
    res.status(200).json(categoryData);
  } catch (err) {
    res.status(400).json(err);
  }
});
```

```md
Delete routes once again worked in a similar fashion, they identified by id and used sequelize destroy to remove the object. Here is another example from categories. 
```

```javascript
router.delete('/:id', async (req, res) => {
  // delete a category by its `id` value
  try {
    const categoryData = await Category.destroy({
      where: {
        id: req.params.id
      }
    });

    if (!categoryData) {
      res.status(404).json({ message: 'No category found with this id!' });
      return;
    }

    res.status(200).json(categoryData);
  } catch (err) {
    res.status(500).json(err);
  }
});
```