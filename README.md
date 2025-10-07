from collections import defaultdict

def min_orbs(potion, recipes, memo):
   
    if potion in memo:
        return memo[potion]

   
    if potion not in recipes:
        memo[potion] = 0
        return 0

    min_cost = float("inf")
    for ing_list in recipes[potion]:
         cost = len(ing_list) - 1            
valid = True
        for ing in ing_list:
            c = min_orbs(ing, recipes, memo)
            if c == float("inf"):  
                valid = False
                break
            cost += c
        if valid:
            min_cost = min(min_cost, cost)

    memo[potion] = min_cost
    return min_cost

def solve():
    n = int(input().strip())
    recipes = defaultdict(list)

    for _ in range(n):
        line = input().strip()
        potion, rhs = line.split("=")
        ingredients = rhs.split("+")
        recipes[potion].append(ingredients)

    target = input().strip()
    memo = {}
    ans = min_orbs(target, recipes, memo)
    print(ans if ans != float("inf") else -1)

if __name__ == "__main__":
    solve()
