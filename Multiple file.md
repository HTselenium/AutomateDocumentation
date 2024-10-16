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
(industrialProductTypeListData[i]['has_children'] as bool)?
```
**if True (has children)** 
goes to industrial_product_portfolio_child_page.dart
```dart
context.push(
'${AppRoutes.productPortfolioIndustrial.path}/product/${industrialProductTypeListData[i]['category']}/${industrialProductTypeListData[i]['product_type_id']}/${industrialProductTypeListData[i]['product_type_id']}',
extra: {
 'subtype_id': industrialProductTypeListData[i]['product_type_id'].toString(),
 'subtype_name':industrialProductTypeListData[i]['product_type'].toString(),
 'products': industrialProductTypeListData[i]['products'],
},
```
**if False (does not have children)** 
goes to industrial_product_portfolio_sub_child_page.dart

```dart
context.push(
'${AppRoutes.productPortfolioIndustrial.path}/product/${industrialProductTypeListData[i]['category']}/${industrialProductTypeListData[i]['product_type_id']}/',
extra: {
 'product_type_id':industrialProductTypeListData[i]['product_type_id'].toString(),
 'product_type':industrialProductTypeListData[i]['product_type'].toString(),
 'product_type_amount':industrialProductTypeListData[i]['product_type_amount'].toString(),
},
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
'${AppRoutes.productPortfolioHomeCare.path}/product/${productTypeListData[i]['category']}/${productTypeListData[i]['product_type_id']}/${productTypeListData[i]['product_type_id']}',
extra: {
 'subtype_id': productTypeListData[i]['product_type_id'].toString(),
 'subtype_name': productTypeListData[i]['product_type'].toString(),
 'products': productTypeListData[i]['products'],
},
```
**if False (does not have children)** 
goes to home_care_product_portfolio_sub_child_page.dart

```dart
context.push(
'${AppRoutes.productPortfolioHomeCare.path}/product/${productTypeListData[i]['category']}/${productTypeListData[i]['product_type_id']}/',
extra:```dart
extra: {
 'product_type_id': productTypeListData[i]['product_type_id'].toString(),
 'product_type': productTypeListData[i]['product_type'].toString(),
 'product_type_amount': productTypeListData[i]['product_type_amount'].toString(),
},
```

### Summary of Documentation Update
The legacy documentation for both `industrial_product_portfolio_page.dart` and `home_care_product_portfolio_page.dart` has been updated to reflect the recent changes made in the pull request. The `isSubProduct` and `isFavourite` flags have been set to `true` in the page display sections to align with the new logic. Additionally, the data dispatch sections have been corrected to ensure that the navigation logic matches the updated code, with the correct parameters being passed for both scenarios where a product type has children or does not have children.

This update ensures that the documentation is consistent with the current implementation of the product portfolio pages, providing accurate information for future reference and maintenance.

Done.