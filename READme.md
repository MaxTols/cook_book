    with open('cook.txt') as f:
        cook_book = dict()
        for line in f:
            name_cook = line.strip()
            cook_count = int(f.readline())
            cook_list = list()
            for i in range(cook_count):
                ingredients = f.readline().strip()
                ingredient_name, quantity, measure = ingredients.split(' | ')
                cook_list.append({
                    'ingredient_name': ingredient_name,
                    'quantity': int(quantity),
                    'measure': measure
                })
            f.readline()
            cook_book[name_cook] = cook_list
    print(cook_book)


    def get_shop_list_by_dishes(dishes, person_count):
        cook_dict = dict()
        for dish in dishes:
            if dish in cook_book:
                for ingr in cook_book[dish]:
                    ingr_list = dict()
                    if ingr['ingredient_name'] not in cook_dict:
                        ingr_list['measure'] = ingr['measure']
                        ingr_list['quantity'] = ingr['quantity'] * person_count
                        cook_dict[ingr['ingredient_name']] = ingr_list
                    else:
                        cook_dict[ingr['ingredient_name']]['quantity'] = cook_dict[ingr['ingredient_name']]['quantity'] + \
                                                                ingr['quantity'] * person_count
            else:
                print('Такого блюда нет в книге!')
        return cook_dict

    dishes = ['Омлет', 'Фахитос']
    person_count = 2
    print(get_shop_list_by_dishes(dishes, person_count))