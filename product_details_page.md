## product_details_page.dart

- ### initState

```dart
void initState() {
    super.initState();
    try {
      final prd = int.tryParse(widget.prd) ?? 0; // Using tryParse with a fallback value.
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
    } on FormatException {
      print('Error: The provided "prd" value is not a valid integer.');
    } catch (e) {
      print('An unexpected error occurred: $e');
    }
  }
```

- ### data dispatch
go to claims_group_page.dart page
```dart
 ${AppRoutes.productPortfolioHomeCare.path}/product/${widget.category}/${prd}/${prd}/${prd}/${prd}/$prodName',
 extra: claimsList,
);
```