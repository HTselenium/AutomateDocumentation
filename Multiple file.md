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
id: industrialProductTypeListData[i]['product_type_id'].toString(),
productName: industrialProductTypeListData[i]['product_type'].toString(),
productNum: industrialProductTypeListData[i]['product_type_amount'].toString(),
isSubProduct: true,
isFavourite: true,
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
 
 '${AppRoutes.productPortfolioIndustrial.path}/product/${industrialProductTypeListData[i]['category']}/${industrialProductTypeListData[i]['product_type_id']}/',
extra: {
 'product_type_id':industrialProductTypeListData[i]['product_type_id'].toString(),
 'product_type':industrialProductTypeListData[i]['product_type'].toString(),
 'product_type_amount':industrialProductTypeListData[i]['product_type_amount'].toString(),
},
```
**if False (does not have children)** 
goes to industrial_product_portfolio_sub_child_page.dart

```dart
context.push(
'${AppRoutes.productPortfolioIndustrial.path}/product/${industrialProductTypeListData[i]['category']}/${industrialProductTypeListData[i]['product_type_id']}/${industrialProductTypeListData[i]['product_type_id']}',
extra: {
 'product_type_id': industrialProductTypeListData[i]['product_type_id'].toString(),
 'product_type':industrialProductTypeListData[i]['product_type'].toString(),
 'product_type_amount':industrialProductTypeListData[i]['product_type_amount'].toString(),
 'products': industrialProductTypeListData[i]['products'],
```
## home_care_product_portfolio_page.dart

- ### initState

```dart
void initState() {
    super.initState();
    final hcProductTypeBox = Hive.box<dynamic>('hcProductTypeBox');
    productTypeListData =
        hcProductTypeBox.values.map((e) => e as Map<String, dynamic>).toList();
  }
```
- ### page display
```dart
id: productTypeListData[i]['product_type_id'].toString(),
productName: productTypeListData[i]['product_type'].toString(),
productNum: productTypeListData[i]['product_type_amount'].toString(),
isSubProduct: true,
isFavourite: true,
category: ProductCategory.all[productTypeListData[i]['category'] as int],
```
- ### data dispatch
**check whether productType has children**
```dart
(productTypeListData[i]['has_children'] as bool)?
```
**if True (has children)** 
goes to home_care_product_portfolio_child_page.dart
```dart
 context.push(
 
 '${AppRoutes.productPortfolioHomeCare.path}/product/${productTypeListData[i]['category']}/${productTypeListData[i]['product_type_id']}/',
extra: {
 'product_type_id': productTypeListData[i]['product_type_id'].toString(),
 'product_type': productTypeListData[i]['product_type'].toString(),
 'product_type_amount':productTypeListData[i]['product_type_amount'].toString(),
},
```
**if False (does not have children)** 
goes to home_care_product_portfolio_sub_child_page.dart

```dart
context.push(
'${AppRoutes.productPortfolioHomeCare.path}/product/${productTypeListData[i]['category']}/${productTypeListData[i]['product_type_id']}',
extra: {
 'subtype_id': productTypeListData[i]['product_type_id'].toString(),
 'subtype_name': productTypeListData[i]['product_type'].toString(),
 'products': productTypeListData[i]['products'],
},
```

### Summary of Legacy Documentation Updates

The legacy documentation for both `industrial_product_portfolio_page.dart` and `home_care_product_portfolio_page.dart` has been updated to reflect the changes made in the pull request. The updates include the setting of `isSubProduct` and `isFavourite` to `true` for all product items, which was not previously documented. Additionally, the routing logic has been updated to include the correct paths and parameters for navigation, ensuring that the application correctly handles product types with and without children.

The `initState` methods remain unchanged, continuing to initialize the state by fetching data from the respective Hive boxes. The page display sections now accurately represent the new state of the `isSubProduct` and `isFavourite` flags. The data dispatch sections have been updated to show the new routing logic, with the correct paths and parameters for both scenarios where a product type has children and when it does not.

These updates ensure that the documentation is in sync with the current state of the codebase, providing accurate information for future development and maintenance.

Done.