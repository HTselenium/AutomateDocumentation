```markdown
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
 'subtype_name': industrialProductTypeListData[i]['product_type'].toString(),
 'products': industrialProductTypeListData[i]['products'],  
},
```
**if False (does not have children)** 
goes to industrial_product_portfolio_sub_child_page.dart

```dart
context.push(
'${AppRoutes.productPortfolioIndustrial.path}/product/${industrialProductTypeListData[i]['category']}/${industrialProductTypeListData[i]['product_type_id']}/',
extra: {
 'product_type_id': industrialProductTypeListData[i]['product_type_id'].toString(),
 'product_type': industrialProductTypeListData[i]['product_type'].toString(),
 'product_type_amount': industrialProductTypeListData[i]['product_type_amount'].toString(),
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

### Summary of Legacy Documentation Updates

The legacy documentation for `home_care_product_portfolio_page.dart` has been updated to reflect the changes made in the pull request. The updates include:

- Setting `isSubProduct` and `isFavourite` properties to `true` for product items in the page display section.
- Adjusting the routing logic in the data dispatch section to handle product types with and without children properly. The URLs and parameters passed to the routing functions have been corrected to match the new routing paths.

These updates ensure that the documentation is consistent with the current implementation of the home care product portfolio page, providing accurate information for future maintenance and development.

Done.