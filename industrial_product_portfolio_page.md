```markdown
## Pull Request Summary

### Title
Refactor: Update for route navigation and variable changes

### Files Affected
- `industrial_product_portfolio_page.dart`

### Lines Affected
- `initState` method
- `page display` section
- `data dispatch` section

### Detailed Changes with Code

#### Description of Changes
The pull request includes a refactor for the `industrial_product_portfolio_page.dart` file, focusing on route navigation and variable changes. The changes aim to improve the clarity and maintainability of the code.

#### Changes in `industrial_product_portfolio_page.dart`
- **After Change:**
- **Lines initState method:**
    ```dart
    void initState() {
        super.initState();
        final industryProductTypeBox = Hive.box<dynamic>('industryProductTypeBox');
        industrialProductTypeListData = industryProductTypeBox.values
            .map((e) => e as Map<String, dynamic>)
            .toList();
      }
    ```
- **Lines page display section:**
    ```dart
    id: industrialProductTypeListData[i]['product_type_id'].toString(),
    productName: industrialProductTypeListData[i]['product_type'].toString(),
    productNum: industrialProductTypeListData[i]['product_type_amount'].toString(),
    isSubProduct: false,
    isFavourite: false,
    category: ProductCategory.all[industrialProductTypeListData[i]['category'] as int],
    ```
- **Lines data dispatch section:**
    ```dart
    // Check whether productType has children
    industrialProductTypeListData[i]['has_children']
    // If True (has children), goes to industrial_product_portfolio_child_page.dart
    context.push(
     '${AppRoutes.productPortfolioIndustrial.path}/product/${industrialProductTypeListData[i]['category']}/${industrialProductTypeListData[i]['product_type_id']}/',
    extra: {
     'product_type_id':industrialProductTypeListData[i]['product_type_id'].toString(),
     'product_type':industrialProductTypeListData[i]['product_type'].toString(),
     'product_type_amount':industrialProductTypeListData[i]['product_type_amount'].toString(),
    },
    // If False (does not have children), goes to industrial_product_portfolio_sub_child_page.dart
    context.push(
    '${AppRoutes.productPortfolioIndustrial.path}/product/${industrialProductTypeListData[i]['category']}/${industrialProductTypeListData[i]['product_type_id']}/${industrialProductTypeListData[i]['product_type_id']}',
    extra: {
     'subtype_id': industrialProductTypeListData[i]['product_type_id'].toString(),
     'subtype_name':industrialProductTypeListData[i]['product_type'].toString(),
     'products': industrialProductTypeListData[i]['products'],
    ```
    
### Summary of Changes
The pull request includes updates to the `industrial_product_portfolio_page.dart` file, specifically in the `initState` method, `page display` section, and `data dispatch` section. The refactor aims to improve the code's readability and maintainability, particularly in the areas of route navigation and variable naming.

### Note
The provided code snippets reflect the current state of the `industrial_product_portfolio_page.dart` file after the refactor. For a complete review, the actual code differences (diffs) are required. Without them, we cannot accurately describe what has been changed, added, or removed in this pull request.
```