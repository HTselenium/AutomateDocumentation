
## product_details_page.dart

- ### initState

```dart
void initState() {
    super.initState();
    final prd = int.parse(widget.prd);
    if (widget.key.toString().contains('product-portfolio-industrial')) {
      final industryProductBox = Hive.box<dynamic>('industryProductBox');
      _productData = industryProductBox.get(prd) as Map<String, dynamic>;
      if (_productData.keys.contains('application_group')) {
        claimsList = _productData['application_group'] as List;
      }
    } else if (widget.key.toString().contains('product-portfolio-home-care')) {
      final hcProductBox = Hive.box<dynamic>('hcProductBox');
      _productData = hcProductBox.get(prd) as Map<String, dynamic>;
      if (_productData.keys.contains('application_group')) {
        claimsList = _productData['application_group'] as List;
      }
    }
  }
```

- ### data dispatch
go to claims_group_page.dart page
```dart
 ${AppRoutes.productPortfolioHomeCare.path}/product/${widget.category}/${product.prd}/${product.prd}/${product.prd}/${product.prd}/$prodName',
 extra: claimsList,
);
```
 
