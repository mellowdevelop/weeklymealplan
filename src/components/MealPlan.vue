<template>
  <div class="w-full flex justify-center">
    <div class="w-full mt-8">
      <button @click="generateMealPlan" class="mb-4 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Generate New Plan
      </button>

      <div class="overflow-x-auto">
        <table class="min-w-full bg-white divide-y divide-gray-200 shadow-sm">
          <thead class="bg-gray-500 text-white">
            <tr>
              <th class="px-6 py-3 text-left text-xs leading-4 font-medium uppercase tracking-wider">
                Dag
              </th>
              <th class="px-6 py-3 text-left text-xs leading-4 font-medium uppercase tracking-wider">
                Ontbijt
              </th>
              <th class="px-6 py-3 text-left text-xs leading-4 font-medium uppercase tracking-wider">
                Lunch
              </th>
              <th class="px-6 py-3 text-left text-xs leading-4 font-medium uppercase tracking-wider">
                Avondeten
              </th>
            </tr>
          </thead>
          <tbody class="bg-white divide-y divide-gray-200">
            <tr v-for="(meal, day) in mealPlan" :key="day" class="hover:bg-gray-100" :class="{'bg-green-100': meal.locked}">
              <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 font-medium text-gray-900">
                {{ day }}
              </td>
              <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-500">
                {{ meal.breakfast }}
              </td>
              <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-500">
                {{ meal.lunch }} 
              </td>
              <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 text-gray-500">
                {{ meal.dinner }}
              </td>
              <td class="px-6 py-4 whitespace-no-wrap text-sm leading-5 font-medium text-gray-900">
                <button @click="meal.locked = !meal.locked" class="px-4 py-2 font-bold text-white rounded-lg shadow-lg hover:bg-blue-400" :class="{'bg-blue-500': !meal.locked, 'bg-green-500': meal.locked}">
                  {{ meal.locked ? '🔓 Unlock' : '🔒 Lock' }}
                </button>
              </td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, reactive } from 'vue';

export default {
  name: 'MealPlan',
  setup() {
    const breakfasts = reactive([    "Tiramisu overnight oats",
    "Scrambled tofu",
    "Tosti",
    "Roerbak ei",
    "Pannenkoeken",
    "Crackertje met huttekäse en kaas",
    "Aarbei cheesecake overnight oats",
    "Gegrilde vis",
    "Gebakken ei",
    "Omelet",
    "Frittata",
    "Haver + banaan + kwark",
    "Gegrilde worstjes",
    "Ham/kaas",
    "Wentelteefjes",
    "Smoothiebowl",
    "Gebakken ei",
    "Bagels met spek en kaas en ei",
    "Avocado toast",
    "Bagel met kruidenkaas en zalm",
    "Bagel met kruidenkaas en komkommer",
    "Toast met tonijnsalade",
    "Croissant"]);
    const lunches = reactive(["Carpaccio",
    "Bibimbap",
    "Quesadillas",
    "Couscoussalade",
    "Knakworst",
    "Nasi",
    "Wrap met kipfilet en kruidenkaas",
    "Zalm",
    "Onigiri",
    "Foccaccia",
    "Kimbap",
    "Gezond",
    "Gebakken ei",
    "Tosti",
    "Bagel met zalm en kruidenkaas",
    "Frikandelbroodje",
    "Kaasbroodje",
    "Hamburgerbroodje",
    "Caprese",
    "Bagel met kruidenkaas en komkommer",
    "Bruscetta met tomaten en avocado"]);
    const dinners = reactive([    "Gehakt wraps",
    "Biefstuk met brocolli",
    "Burgers",
    "Chili con carne",
    "Mac N Cheese",
    "Lasange",
    "Risotto",
    "Orzo salade",
    "Erwtensoep",
    "Ramen",
    "Fajitas",
    "Tjap tjoy",
    "Pizza",
    "Hutspot",
    "Quiche",
    "Spaghetti bolognese",
    "Nasi",
    "Ceasar salad",
    "Tomatensoep",
    "Bibimyun",
    "Burritos",
    "Nua pad prik",
    "Fried chicken",
    "Shakshuka",
    "Parelcouscous met aubergine",
    "Pasta pesto",
    "Bibimbap",
    "Couscoussalade",
    "Broccolisoep",
    "Bami",
    "Zalmwraps",
    "Tofu met soja en gember",
    "(Airfryer) snacks",
    "Kapsalon",
    "Gnocchi",
    "Sushi",
    "Pompoensoep",
    "Sesam noedels",
    "Quesadillas",
    "Hotpot",
    "Carbonara",
    "Burrito bowl",
    "Linzensoep",
    "Udon",
    "Pita shoarma",
    "Lasagnette",
    "Poké bowl",
    "Brocoli cheddar soep",
    "Pasta bake",
    "Chicken biriyani",
    "Macaroni",
    "Indiase curry",
    "Thaise groene curry"]);

    const mealPlan = reactive({
      Maandag: {breakfast: null, lunch: null, dinner: null, locked:false},
      Dinsdag: {breakfast: null, lunch: null, dinner: null, locked:false},
      Woensdag: {breakfast: null, lunch: null, dinner: null, locked:false},
      Donderdag: {breakfast: null, lunch: null, dinner: null, locked:false},
      Vrijdag: {breakfast: null, lunch: null, dinner: null, locked:false},
      Zaterdag: {breakfast: null, lunch: null, dinner: null, locked:false},
      Zondag: {breakfast: null, lunch: null, dinner: null, locked:false},
    });

    const getRandomMeal = (meals) => {
  const index = Math.floor(Math.random() * meals.length);
  const meal = meals[index];
  meals.splice(index, 1); // Remove the selected meal from the array
  return meal;
};

const generateMealPlan = () => {
  const breakfastsCopy = [...breakfasts];
  const lunchesCopy = [...lunches];
  const dinnersCopy = [...dinners];

  for (const day in mealPlan) {
    if (!mealPlan[day].locked) {
      mealPlan[day] = {
        ...mealPlan[day],
        breakfast: getRandomMeal(breakfastsCopy),
        lunch: getRandomMeal(lunchesCopy),
        dinner: getRandomMeal(dinnersCopy),
      };
    }
  }
};

    return { mealPlan, generateMealPlan };
  },
};
</script>

<style scoped>
  /* Your styles go here */
</style>