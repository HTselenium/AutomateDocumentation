## claims_page.dart

- ### initState

```dart
void initState() {
    super.initState();
    final hcClaimsBox = Hive.box<dynamic>('hcClaimsBox');
    claimsDataList =
        hcClaimsBox.values.map((e) => e as Map<String, dynamic>).toList();
  }
```
- ### page display
```dart
id: claimsDataList[i]['application_id'].toString(),
productName: claimsDataList[i]['application'].toString(),
productNum:claimsDataList[i]['application_amount'].toString(),
isFavourite: false,
isSubProduct: false,
category: ProductCategory.categoryOrange,
```
- ### data dispatch
go to sub_claim_page.dart page
```dart
context.push(
'${AppRoutes.claims.path}/subclaim/${claimsDataList[i]['application_id']}',
extra: {
'application': claimsDataList[i]['application'],
'application_id': claimsDataList[i]['application_id'],
'application_amount': claimsDataList[i]['application_amount'],},
);```

