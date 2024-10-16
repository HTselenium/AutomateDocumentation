```markdown
## Pull Request Summary

### Title
Multiple files branch

### Files Affected
- Changes not found, unable to list affected files.

### Lines Affected
- Changes not found, unable to specify affected lines.

### Detailed Changes with Code

#### Description of Changes
The pull request does not include specific details about the changes made. It appears to be a code refactor, but without the actual diff, it's not possible to provide a detailed description or the new code.

#### Changes in `<affected_class_or_method_name>`
- **After Change:**
- **Lines <start_line>-<end_line>:**
    ```<programming_language>
    // Changes not found, unable to provide new code snippet.
    ```

### Summary of Changes
Without the specific changes, a high-level summary cannot be provided. The pull request title suggests a refactor was performed on multiple files, but the lack of details and code changes in the provided information makes it impossible to summarize the modifications.

Please provide the actual diff or more information about the changes for a detailed summary.
```

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
 'subtype_id': industrialProductTypeListData[i]['product_type_id'].toString(),
 'subtype_name':industrialProductTypeListData[i]['product_type'].toString(),
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
isSubProduct: false,
isFavourite: false,
category: ProductCategory.all[productTypeListData[i]['category'] as int```
],
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
'${AppRoutes.productPortfolioHomeCare.path}/product/${productTypeListData[i]['category']}/${productTypeListData[i]['product_type_id']}/${productTypeListData[i]['product_type_id']}',
extra: {
 'subtype_id': productTypeListData[i]['product_type_id'].toString(),
 'subtype_name': productTypeListData[i]['product_type'].toString(),
 'products': productTypeListData[i]['products'],
},
```

Done.