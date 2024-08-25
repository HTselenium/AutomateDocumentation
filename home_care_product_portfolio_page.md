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
productNum: (productTypeListData[i]['has_children'] as bool) ? productTypeListData[i]['product_type_amount'].toString() : '0',
isSubProduct: (productTypeListData[i]['has_children'] as bool),
isFavourite: false,
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
'product_type_id': productTypeListData[i]['product_type_id'].toString(),
'product_type': productTypeListData[i]['product_type'].toString(),
```
**if False (does not have children)** 
goes to home_care_product_portfolio_sub_child_page.dart

```dart
'product_type_id': productTypeListData[i]['product_type_id'].toString(),
'product_type': productTypeListData[i]['product_type'].toString(),
```