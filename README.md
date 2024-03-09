# Khan Sir Recipe Food App


Khan Sir Food Recipe App

![alt text](image.png)


![alt text](image-1.png)


![alt text](image-2.png)

## Technologies

- HTML
- Css
- Javascript

### TheMealDB API

Khan Sir Recipe integrates seamlessly with TheMealDB API to fetch an extensive variety of recipes. As a publicly accessible API, it provides a wealth of culinary information, allowing users to discover and explore diverse dishes effortlessly.

# Features


### Search recipes by name

* Users are able to type into a search bar to search for recipes by name

### Filter recipes by category

* Users are able to filter recipes by category

### Filter recipes by area

* Users are able to filter recipes by areas of the world (countries)

### Lookup a random recipe

* Users are able to cycle through random recipes on click

### List all recipes by the first letter

* Users are able to list all recipes whose name begins with the clicked letter

### View recipe details

* Users are able to click on any recipe card to view the details of the clicked recipe (name, ingredients, etc.)

### Save recipes

* Users are able to save recipes which can be viewed later in the favorites page


```javascript
export async function getMealsByCategory(setState, category) {
  try {
    const url = `https://www.themealdb.com/api/json/v1/1/filter.php?c=${category}`
    const resp = await fetch(url);
    const data = await resp.json();

    const newDataArray = await Promise.all(
      data.meals.map(async (meal) => {
        const resp = await fetch(`https://www.themealdb.com/api/json/v1/1/lookup.php?i=${meal.idMeal}`);
        const data = await resp.json();
        return await data.meals[0];
      })
    )

    setState(newDataArray)
  } catch(err) {
    console.error(err)
  }
}
```

This function was able to return data that originally looked like this:

```json
[
        {
            "strMeal": "Baked salmon with fennel & tomatoes",
            "strMealThumb": "https://www.themealdb.com/images/media/meals/1548772327.jpg",
            "idMeal": "52959"
        },
        {
            "strMeal": "Cajun spiced fish tacos",
            "strMealThumb": "https://www.themealdb.com/images/media/meals/uvuyxu1503067369.jpg",
            "idMeal": "52819"
        },
        {
            "strMeal": "Escovitch Fish",
            "strMealThumb": "https://www.themealdb.com/images/media/meals/1520084413.jpg",
            "idMeal": "52944"
        },

        ...

]
```

And in the end, looked like this:

```json
[
       {
           "idMeal": "52959",
           "strMeal": "Baked salmon with fennel & tomatoes",
           "strCategory": "Seafood",
           "strArea": "British",
            ...
       },
       {
           "idMeal": "52944",
           "strMeal": "Escovitch Fish",
           "strCategory": "Seafood",
           "strArea": "Jamaican",
            ...
       },

       ...

]
```

