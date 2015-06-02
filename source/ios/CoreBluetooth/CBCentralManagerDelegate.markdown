---
layout: page
title: "CBCentralManagerDelegate"
date: 2014-04-09 10:50
comments: true
sharing: true
footer: true
---




## CBCentralManagerDelegate


#### - (void)centralManagerDidUpdateState:(CBCentralManager *)central;
centralManagerのステートが変更された時。
`central.state`プロパティを確認。

| Column1(left) | Column2(center) |
| :------------ | :-------------: |
|CBCentralManagerStateUnknown |
|CBCentralManagerStateResetting |
|CBCentralManagerStateUnsupported |
|CBCentralManagerStateUnauthorized |
|CBCentralManagerStatePoweredOff |
|CBCentralManagerStatePoweredOn |





#### - (void)centralManager:(CBCentralManager *)central didDiscoverPeripheral:(CBPeripheral *)peripheral advertisementData:(NSDictionary *)advertisementData RSSI:(NSNumber *)RSSI;



{
    MYBeacon *beacon = [[MYBeacon alloc] initWithPeripheral:peripheral advertisementData:advertisementData RSSI:RSSI];
    [self.peripheralArray addObject:beacon];
//    NSLog(@"NAME => %@",peripheral.name);
//    NSLog(@"%@",advertisementData);
    [self.tableView reloadData];
}

```
- (void)centralManager:(CBCentralManager *)central willRestoreState:(NSDictionary *)dict;
```

 {
    NSLog(@"1");
}

- (void)centralManager:(CBCentralManager *)central didRetrievePeripherals:(NSArray *)peripherals{
    NSLog(@"2");
}

- (void)centralManager:(CBCentralManager *)central didRetrieveConnectedPeripherals:(NSArray *)peripherals{
    NSLog(@"3");
}

- (void)centralManager:(CBCentralManager *)central didConnectPeripheral:(CBPeripheral *)peripheral{
    NSLog(@"4");
    // 外部デバイスとの接続完了を通知
//    [self peripheralManagerDidConnectPeripheral:self];

    // 探索するサービスを指定
//    NSArray *services = [NSArray arrayWithObjects:[CBUUID UUIDWithString:BLEServiceBattery], nil];
    // サービスの探索を開始

//    bsc.services = periphe;

    peripheral_.delegate = self;

    [peripheral discoverServices:nil];
//    [peripheral discoverCharacteristics:nil forService:];
    NSLog(@"service = %@",peripheral.services);
//    [peripheral discoverIncludedServices:nil forService:peripheral.services];
}

- (void)centralManager:(CBCentralManager *)central didFailToConnectPeripheral:(CBPeripheral *)peripheral error:(NSError *)error{
    NSLog(@"5");
}

- (void)centralManager:(CBCentralManager *)central didDisconnectPeripheral:(CBPeripheral *)peripheral error:(NSError *)error{
    NSLog(@"6");
    [self.navigationController popToRootViewControllerAnimated:YES];
}
