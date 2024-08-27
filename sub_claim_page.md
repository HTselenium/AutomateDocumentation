## sub_claim_page.dart

- ### initState

```dart
void initState() {
    super.initState();
    _id = widget.id;
    _applicationInfo = widget.applicationInfo;

    final hcClaimsBox = Hive.box<dynamic>('hcClaimsBox');
    final functionObj = hcClaimsBox.values.firstWhere(
      (element) => (element as Map)['application_id'].toString() == _id,
    );
    functionClaimList = ((functionObj as Map)['children'] as List)
        .map((e) => e as Map<String, dynamic>)
        .toList();
  }
```
- ### page display
```dart
id: functionClaimList[i]['function_claim_id'].toString(),
productName: functionClaimList[i]['function_claim_name'].toString(),
productNum: functionClaimList[i]['function_claim_amount'].toString(),
isFavourite: false,
isSubProduct: true,
category: ProductCategory.categoryRed,
```
- ### data dispatch
go to claims_claim_page.dart page
```dart
context.push(
'${AppRoutes.claims.path}/subclaim/$_id/${functionClaimList[i]['function_claim_id']}',
extra: {
'function_claim_name': functionClaimList[i]['function_claim_name'],
'function_claim_id': functionClaimList[i]['function_claim_id'],
'function_claim_amount': functionClaimList[i]['function_claim_amount'],
'application_id': _id,
},
);```

