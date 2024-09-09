## industrial_product_portfolio_page.dart

- ### initState

```dart
void initState() {
    super.initState();
    final industryProductTypeBox = Hive.box<dynamic>('industryProductTypeBox');
    industrialProductTypeListData = industryProductTypeBox.values
        .map((e) => e as Map<String, dynamic>)
        .toList();
  }
```
- ### page display
```dart
id: industrialProductTypeListData[i]['subtype_id'].toString(),
productName: industrialProductTypeListData[i]['subtype_name'].toString(),
productNum: (industrialProductTypeListData[i]['products'] as List).length.toString(),
isSubProduct: false,
isFavourite: false,
category: ProductCategory.all[industrialProductTypeListData[i]['category'] as int],

```
- ### data dispatch
**check whether productType has children**
```dart
industrialProductTypeListData[i]['has_children']
```
**if True (has children)** 
goes to industrial_product_portfolio_child_page.dart
```dart
 context.push(
 
 '${AppRoutes.productPortfolioIndustrial.path}/product/${industrialProductTypeListData[i]['category']}/${industrialProductTypeListData[i]['subtype_id']}/',
extra: {
 'subtype_id':industrialProductTypeListData[i]['subtype_id'].toString(),
 'subtype_name':industrialProductTypeListData[i]['subtype_name'].toString(),
 'products': industrialProductTypeListData[i]['products'],
},
```
**if False (does not have children)** 
goes to industrial_product_portfolio_sub_child_page.dart

```dart
context.push(
'${AppRoutes.productPortfolioIndustrial.path}/product/${industrialProductTypeListData[i]['category']}/${industrialProductTypeListData[i]['subtype_id']}/${industrialProductTypeListData[i]['subtype_id']}',
extra: {
 'subtype_id': industrialProductTypeListData[i]['subtype_id'].toString(),
 'subtype_name':industrialProductTypeListData[i]['subtype_name'].toString(),
 'products': industrialProductTypeListData[i]['products'],
```
