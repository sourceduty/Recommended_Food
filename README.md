## Recommended_Food

🍔 Software concept for generating new, related and recommended meals.

![Meals](https://github.com/sourceduty/Recommended_Food/assets/123030236/fcc1396f-7f44-4291-81c2-616dcef8dba3)

## CONCEPT

1. Choose your 10 favorite meals from a searchable meal index.
2. Generate a list of 10 new, related and recommended meals.

## EXPERIMENT

```
import requests

def search_meal_by_name(meal_name):
    search_url = f'https://www.themealdb.com/api/json/v1/1/search.php?s={meal_name}'
    response = requests.get(search_url)
    data = response.json()
    return data

def get_user_meals():
    user_meals = []
    for i in range(10):
        meal_name = input(f"Enter the name of your favorite meal {i + 1}: ")
        user_meals.append(meal_name)
    return user_meals

def get_recommendations(user_meals):
    recommendations = []
    for meal_name in user_meals:
        meal_data = search_meal_by_name(meal_name)
        if meal_data['meals']:
            for meal in meal_data['meals']:
                recommendation = meal['strMeal']
                if recommendation not in user_meals and recommendation not in recommendations:
                    recommendations.append(recommendation)
    
    return recommendations[:10]  # Get the top 10 unique recommendations

def main():
    print("Welcome to the Meal Recommender System!")
    user_meals = get_user_meals()
    recommendations = get_recommendations(user_meals)

    print("\nRecommended Meals:")
    for i, meal in enumerate(recommendations):
        print(f"{i + 1}. {meal}")

if __name__ == "__main":
    main()
```
