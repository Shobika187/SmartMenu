# SmartMenu
### program:
```
import pandas as pd

# Load the dataset (this is the dataset you provided in CSV format)
df = pd.read_csv('smart_menu_system_data_expanded.csv')

# Function to suggest a dish based on user input
def suggest_dish(preferred_cuisine, dietary_restriction, preferred_spice_level):
    # Filter the dataset based on user preferences
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Dietary_Restrictions'] == dietary_restriction) &
        (df['Preferred_Spice_Level'] == preferred_spice_level)
    ]

    # If there's a match, return the favorite dish from the filtered dataset
    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]  # Take the first matching dish
    else:
        return "Sorry, no matching dish found."

# Example usage
preferred_cuisine = input("Enter preferred cuisine (e.g., Italian, Indian, Chinese): ")
dietary_restriction = input("Enter dietary restriction (e.g., None, Vegetarian, Vegan): ")
preferred_spice_level = input("Enter preferred spice level (e.g., Mild, Medium, Hot): ")

# Get the recommended dish
recommended_dish = suggest_dish(preferred_cuisine, dietary_restriction, preferred_spice_level)

# Output the recommended dish
print(f"Recommended dish: {recommended_dish}")


import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

# Part 1: Load the dataset
def load_dataset(file_path):
    df = pd.read_csv(file_path)
    return df

# Part 2: User input collection
def collect_user_input():
    preferred_cuisine = input("Enter preferred cuisine (e.g., Italian, Indian, Chinese): ")
    dietary_restriction = input("Enter dietary restriction (e.g., None, Vegetarian, Vegan): ")
    preferred_spice_level = input("Enter preferred spice level (e.g., Mild, Medium, Hot): ")
    meal_type = input("Enter meal type (e.g., Breakfast, Lunch, Dinner, Snacks, Dessert): ")
    return preferred_cuisine, dietary_restriction, preferred_spice_level, meal_type

# Part 3: Dish suggestion logic
def suggest_dish(df, preferred_cuisine, dietary_restriction, preferred_spice_level, meal_type):
    # Try to match all user preferences
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Dietary_Restrictions'] == dietary_restriction) &
        (df['Preferred_Spice_Level'] == preferred_spice_level) &
        (df['Meal_Type'] == meal_type)
    ]

    # Primary search: All conditions match
    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # Fallback 1: Match based on cuisine, restriction, and meal type (ignore spice level)
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Dietary_Restrictions'] == dietary_restriction) &
        (df['Meal_Type'] == meal_type)
    ]

    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # Fallback 2: Match based on cuisine and meal type only
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Meal_Type'] == meal_type)
    ]

    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # No match found
    return "Sorry, no matching dish found."

# Part 4: Data visualization
def visualize_data(df):
    # Visualize cuisine distribution
    plt.figure(figsize=(10, 6))
    sns.countplot(x="Preferred_Cuisine", data=df, order=df['Preferred_Cuisine'].value_counts().index)
    plt.title('Cuisine Preference Distribution')
    plt.xticks(rotation=45)
    plt.show()

    # Visualize dietary restriction distribution
    plt.figure(figsize=(10, 6))
    sns.countplot(x="Dietary_Restrictions", data=df, order=df['Dietary_Restrictions'].value_counts().index)
    plt.title('Dietary Restriction Distribution')
    plt.xticks(rotation=45)
    plt.show()

    # Visualize meal type distribution
    plt.figure(figsize=(10, 6))
    sns.countplot(x="Meal_Type", data=df, order=df['Meal_Type'].value_counts().index)
    plt.title('Meal Type Distribution')
    plt.xticks(rotation=45)
    plt.show()

# Main flow of the system
if __name__ == "__main__":
    # Load the dataset
    df = load_dataset('smart_menu_system_data_expanded_v2.csv')

    # Visualize the dataset
    visualize_data(df)

    # Collect user inputs
    preferred_cuisine, dietary_restriction, preferred_spice_level, meal_type = collect_user_input()

    # Recommend a dish based on the inputs
    recommended_dish = suggest_dish(df, preferred_cuisine, dietary_restriction, preferred_spice_level, meal_type)

    # Output the recommended dish
    print(f"Recommended dish: {recommended_dish}")


# Updated dish suggestion logic
def suggest_dish(df, preferred_cuisine, dietary_restriction, preferred_spice_level, meal_type):
    # Try to match all user preferences
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Dietary_Restrictions'] == dietary_restriction) &
        (df['Preferred_Spice_Level'] == preferred_spice_level) &
        (df['Meal_Type'] == meal_type)
    ]

    # Primary search: All conditions match
    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # Fallback 1: Match based on cuisine, restriction, and meal type (ignore spice level)
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Dietary_Restrictions'] == dietary_restriction) &
        (df['Meal_Type'] == meal_type)
    ]

    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # Fallback 2: Match based on cuisine and meal type only
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Meal_Type'] == meal_type)
    ]

    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # Fallback 3: Match based on cuisine only
    filtered_df = df[df['Preferred_Cuisine'] == preferred_cuisine]

    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # No match found
    return "Sorry, no matching dish found."
import pandas as pd
import random

# Sample dataset creation
cuisines = ['Chinese', 'Italian', 'Indian', 'Mexican', 'Japanese', 'Thai', 'Mediterranean', 'American']
dietary_restrictions = ['None', 'Vegetarian', 'Vegan', 'Gluten-Free']
spice_levels = ['Mild', 'Medium', 'Hot']
meal_types = ['Breakfast', 'Lunch', 'Dinner', 'Snacks', 'Dessert']
dishes = [
    'Stir-fry', 'Pizza', 'Biryani', 'Tacos', 'Sushi',
    'Pad Thai', 'Falafel', 'Burger', 'Pasta', 'Soup',
    'Salad', 'Cake', 'Vegan Hotpot', 'Spicy Tofu Stir-fry',
    'Kung Pao Tofu', 'Sweet and Sour Tofu'
]

# Creating a larger dataset with specific entries
data = []
for i in range(1000):  # Adjust this number for more entries
    cuisine = random.choice(cuisines)
    dietary_restriction = random.choice(dietary_restrictions)
    spice_level = random.choice(spice_levels)
    meal_type = random.choice(meal_types)

    # Create a dish name based on cuisine and dietary restrictions
    if cuisine == 'Chinese' and dietary_restriction == 'Vegan' and spice_level == 'Hot' and meal_type == 'Lunch':
        dish = random.choice(['Spicy Tofu Stir-fry', 'Vegan Hotpot', 'Kung Pao Tofu'])
    elif cuisine == 'Chinese' and dietary_restriction == 'None' and spice_level == 'Medium' and meal_type == 'Lunch':
        dish = 'Kung Pao Chicken'
    elif cuisine == 'Italian' and dietary_restriction == 'Vegan' and spice_level == 'Mild' and meal_type == 'Lunch':
        dish = 'Vegan Pasta'
    else:
        dish = random.choice(dishes) + f" ({cuisine})"  # Default dish

    data.append([cuisine, dietary_restriction, spice_level, meal_type, dish])

# Convert to DataFrame
df = pd.DataFrame(data, columns=['Preferred_Cuisine', 'Dietary_Restrictions', 'Preferred_Spice_Level', 'Meal_Type', 'Favorite_Dish'])

# Function to suggest a dish based on user preferences
def suggest_dish(df, preferred_cuisine, dietary_restriction, preferred_spice_level, meal_type):
    # Primary search: Match all user preferences
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Dietary_Restrictions'] == dietary_restriction) &
        (df['Preferred_Spice_Level'] == preferred_spice_level) &
        (df['Meal_Type'] == meal_type)
    ]

    # If a dish is found, return it
    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # Fallback: Match cuisine and meal type only (ignore dietary and spice)
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Meal_Type'] == meal_type)
    ]

    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # Fallback: Match cuisine only
    filtered_df = df[df['Preferred_Cuisine'] == preferred_cuisine]

    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # No match found
    return "Sorry, no matching dish found."

# Test the function with user input
preferred_cuisine = "Chinese"
dietary_restriction = "Vegan"
preferred_spice_level = "Hot"
meal_type = "Lunch"

# Get the recommended dish
recommended_dish = suggest_dish(df, preferred_cuisine, dietary_restriction, preferred_spice_level, meal_type)

print("Recommended dish:", recommended_dish)

import pandas as pd
import random

# Sample dataset creation
cuisines = ['Chinese', 'Italian', 'Indian', 'Mexican', 'Japanese', 'Thai', 'Mediterranean', 'American']
dietary_restrictions = ['None', 'Vegetarian', 'Vegan', 'Gluten-Free']
spice_levels = ['Mild', 'Medium', 'Hot']
meal_types = ['Breakfast', 'Lunch', 'Dinner', 'Snacks', 'Dessert']
dishes = [
    'Stir-fry', 'Pizza', 'Biryani', 'Tacos', 'Sushi',
    'Pad Thai', 'Falafel', 'Burger', 'Pasta', 'Soup',
    'Salad', 'Cake', 'Vegan Hotpot', 'Spicy Tofu Stir-fry',
    'Kung Pao Tofu', 'Sweet and Sour Tofu', 'Kung Pao Chicken', 'Vegan Pasta'
]

# Creating a larger dataset with specific entries
data = []
for i in range(1000):  # Adjust this number for more entries
    cuisine = random.choice(cuisines)
    dietary_restriction = random.choice(dietary_restrictions)
    spice_level = random.choice(spice_levels)
    meal_type = random.choice(meal_types)

    # Create a dish name based on cuisine and dietary restrictions
    if cuisine == 'Chinese' and dietary_restriction == 'Vegan' and spice_level == 'Hot' and meal_type == 'Lunch':
        dish = random.choice(['Spicy Tofu Stir-fry', 'Vegan Hotpot', 'Kung Pao Tofu'])
    elif cuisine == 'Chinese' and dietary_restriction == 'None' and spice_level == 'Medium' and meal_type == 'Lunch':
        dish = 'Kung Pao Chicken'
    elif cuisine == 'Italian' and dietary_restriction == 'Vegan' and spice_level == 'Mild' and meal_type == 'Lunch':
        dish = 'Vegan Pasta'
    else:
        dish = random.choice(dishes) + f" ({cuisine})"  # Default dish

    data.append([cuisine, dietary_restriction, spice_level, meal_type, dish])

# Convert to DataFrame
df = pd.DataFrame(data, columns=['Preferred_Cuisine', 'Dietary_Restrictions', 'Preferred_Spice_Level', 'Meal_Type', 'Favorite_Dish'])

# Function to suggest a dish based on user preferences
def suggest_dish(df, preferred_cuisine, dietary_restriction, preferred_spice_level, meal_type):
    # Primary search: Match all user preferences
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Dietary_Restrictions'] == dietary_restriction) &
        (df['Preferred_Spice_Level'] == preferred_spice_level) &
        (df['Meal_Type'] == meal_type)
    ]

    # If a dish is found, return it
    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # Fallback: Match cuisine and meal type only (ignore dietary and spice)
    filtered_df = df[
        (df['Preferred_Cuisine'] == preferred_cuisine) &
        (df['Meal_Type'] == meal_type)
    ]

    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # Fallback: Match cuisine only
    filtered_df = df[df['Preferred_Cuisine'] == preferred_cuisine]

    if not filtered_df.empty:
        return filtered_df['Favorite_Dish'].iloc[0]

    # No match found
    return "Sorry, no matching dish found."

# Get user input
preferred_cuisine = input("Enter preferred cuisine (e.g., Italian, Indian, Chinese): ")
dietary_restriction = input("Enter dietary restriction (e.g., None, Vegetarian, Vegan): ")
preferred_spice_level = input("Enter preferred spice level (e.g., Mild, Medium, Hot): ")
meal_type = input("Enter meal type (e.g., Breakfast, Lunch, Dinner, Snacks, Dessert): ")

# Get the recommended dish
recommended_dish = suggest_dish(df, preferred_cuisine, dietary_restriction, preferred_spice_level, meal_type)

# Display the recommendation
print("Recommended dish:", recommended_dish)






```
### Output:
![image](https://github.com/user-attachments/assets/c543817b-cb8e-46de-94b2-1aa664999d59)

![image](https://github.com/user-attachments/assets/506b03a5-94f5-427b-9b50-e61bb71e27e1)

![image](https://github.com/user-attachments/assets/ac62f9d5-0328-4e6f-a3ae-2dc3a38355bf)


![image](https://github.com/user-attachments/assets/2c694252-af56-467d-8f6d-e6c7875b8d4b)


![image](https://github.com/user-attachments/assets/411256a4-21f6-4b5e-b38d-0b3abb8121a2)

![image](https://github.com/user-attachments/assets/cb741147-ba99-4ee6-a458-fe52c7bdf255)

![image](https://github.com/user-attachments/assets/2c2169f0-e503-4d90-ae3e-5a791ff8cbe5)

![image](https://github.com/user-attachments/assets/11de7ec7-b712-4cbd-8e63-12e5f41f7cc6)

