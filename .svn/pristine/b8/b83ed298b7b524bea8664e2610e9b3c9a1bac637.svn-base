from faker import Faker
from datetime import datetime
import math
import random
import csv
import xlsxwriter


# //////////////////////// GLOBALS ////////////////////////

fake = Faker()
fake_ru = Faker('ru_RU')

Mails = ['@yahoo.com', '@gmail.com', '@yandex.ru', '@mail.ru']
s_countries = ['Россия', 'Украина', 'Белоруссия', 'Казахстан']
catalogs = ['RAL', 'NCS', 'Pantone', 'Monicolor', 'Color-index', 'Symphony', 'Ambiance', 'Eurotrend',
            'Московская палитра', 'Российский каталог образцов цвета лакокрасочных материалов']

chars = '+-/*!&$#?=@<>abcdefghijklnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ1234567890'


# //////////////////////// HELPERS ////////////////////////

def randomChoice(_range, length):
    tmp = []
    while len(tmp) < length:
        x = random.randint(1, _range)
        if x not in tmp:
            tmp.append(x)
    return tmp

def dateDiff(d1, d2):
    d1 = datetime.strptime(d1, "%Y-%m-%d")
    d2 = datetime.strptime(d2, "%Y-%m-%d")
    return ((d2 - d1).days)

def makePassword(length):
    password = ''
    for i in range(length):
        password += random.choice(chars)
    return password

def writeCSV(filename, functionName):
    with open(f'{filename}.csv', 'w', newline='') as f:
        w = csv.writer(f)
        for i in range (0, len(functionName)):
            w.writerow((functionName)[i])

def writeXLS(filename, functionName):
    workbook = xlsxwriter.Workbook(f'{filename}.xlsx')
    worksheet = workbook.add_worksheet()
    row = 0
    col = 0
    for i in range(len(functionName)):
        for j in range(len(functionName[i])):
            item = functionName[i][j]
            worksheet.write(row, col+j, item)
        row += 1
    workbook.close()

def TrueOrFalse(chance):
    result = fake.boolean(chance_of_getting_true=chance)
    if result:
        return 1
    else:
        return 0


# //////////////////////// ENTITIES ////////////////////////

# ///////////// 1000 /////////////
def Buyers(_range):
    buyers_dict = []
    for i in range(1, _range):
        BuyerID = i
        Login = fake.first_name() + f'{math.floor(10000 * math.acosh(i)) + random.randint(1,1000)}' + f'{random.choice(Mails)}'
        Password = makePassword(20)
        buyers_dict.append([BuyerID, Login, Password])
    return buyers_dict
# writeXLS('buyers', Buyers(1001))


# ///////////// 300 /////////////
def NaturalPersons(_range):
    np_dict = []
    B_rand = (randomChoice(1000, _range))
    for i in range(1, _range):
        NP_ID = i
        NP_BuyerID = B_rand[i]
        FullName = fake_ru.name()
        Surname = (FullName.split(' '))[0]
        Name = (FullName.split(' '))[1]
        MiddleName = (FullName.split(' '))[2]
        Phone = '+7 ' + f'({random.randint(100, 999)})' + ' ' + f'{random.randint(100, 999)}' + '-' + f'{random.randint(10, 99)}' + '-' + f'{random.randint(10, 99)}'
        Email = fake.sentence().split(' ')[1] + f'{math.floor(10000 * math.acosh(i)) + random.randint(1,1000)}' + f'{random.choice(Mails)}'
        np_dict.append([NP_ID, NP_BuyerID, Surname, Name, MiddleName, Phone, Email])
    return np_dict
# writeXLS('natural-persons', NaturalPersons(301))

# ///////////// 150 /////////////
def LegalPersons(_range):
    np_dict = []
    B_rand = (randomChoice(1000, _range))
    for i in range(1, _range):
        LP_ID = i
        LP_BuyerID = B_rand[i]
        CompanyName = fake_ru.company()
        Phone = '+7 ' + f'({random.randint(100, 999)})' + ' ' + f'{random.randint(100, 999)}' + '-' + f'{random.randint(10, 99)}' + '-' + f'{random.randint(10, 99)}'
        Fax = '+7 ' + f'({random.randint(100, 999)})' + ' ' + f'{random.randint(100, 999)}' + '-' + f'{random.randint(10, 99)}' + '-' + f'{random.randint(10, 99)}'
        Email = fake.sentence().split(' ')[1] + f'{math.floor(10000 * math.acosh(i)) + random.randint(1,1000)}' + f'{random.choice(Mails)}'
        INN = fake_ru.businesses_inn()
        while len(INN) != 10:
            INN = fake_ru.businesses_inn()
        CRR = fake_ru.bic()
        while len(CRR) != 9:
            CRR = fake_ru.bic()
        BIC = fake_ru.bic()
        while len(BIC) != 9:
            BIC = fake_ru.bic()
        SettlementAccount = fake_ru.checking_account()
        np_dict.append([LP_ID, LP_BuyerID, CompanyName, Phone, Fax, Email, INN, CRR, BIC, SettlementAccount])
    return np_dict
# writeXLS('legal-persons', LegalPersons(151))

# ///////////// 100 /////////////
def Suppliers(_range):
    sp_dict = []
    for i in range(1, _range):
        SupplierID = i
        Supplier_CompanyName = fake_ru.company()[:255]
        Phone = '+7 ' + f'({random.randint(100, 999)})' + ' ' + f'{random.randint(100, 999)}' + '-' + f'{random.randint(10, 99)}' + '-' + f'{random.randint(10, 99)}'
        Fax = '+7 ' + f'({random.randint(900, 999)})' + ' ' + f'{random.randint(100, 999)}' + '-' + f'{random.randint(10, 99)}' + '-' + f'{random.randint(10, 99)}'
        Email = fake.sentence().split(' ')[1] + f'{math.floor(10000 * math.acosh(i)) + random.randint(1,1000)}' + f'{random.choice(Mails)}'
        Site = (fake.sentence().split(' ')[0]).lower() + '.ru'
        INN = fake_ru.businesses_inn()
        if len(INN) == 9:
            INN = f'{INN} + 1'
        CRR = fake_ru.bic()
        while len(CRR) != 9:
            CRR = fake_ru.bic()
        BIC = fake_ru.bic()
        while len(BIC) != 9:
            BIC = fake_ru.bic()
        SettlementAccount = fake_ru.checking_account()
        sp_dict.append([SupplierID, Supplier_CompanyName, Phone, Fax, Email, Site, INN, CRR, BIC, SettlementAccount])
    return sp_dict
# writeXLS('suppliers', Suppliers(101))


# ///////////// 210 /////////////
def Addresses(_range):
    ad_dict = []
    for i in range(1, _range):

        AddressID = i
        if i % 2 == 0:
            NP_BuyerID = random.randint(1, 300)
            LP_BuyerID = 'NULL'
            SupplierID = 'NULL'
        elif i % 5 == 0:
            NP_BuyerID = 'NULL'
            LP_BuyerID = random.randint(1, 150)
            SupplierID = 'NULL'
        else:
            NP_BuyerID = 'NULL'
            LP_BuyerID = 'NULL'
            SupplierID = random.randint(1, 100)
        IsRegistered = TrueOrFalse(20)
        IsActual = TrueOrFalse(20)
        if fake.boolean(chance_of_getting_true=2):
            Country = 'Россия'
        else:
            Country = random.choice(s_countries)
        Region = fake_ru.region()
        City = fake_ru.city_name()
        Street = fake_ru.street_name()
        BuildingNo = f'{random.randint(1, 100)}' + fake_ru.plate_letter()
        Postcode = fake_ru.postcode()
        if fake.boolean(chance_of_getting_true=25) == 1:
            Comment = fake_ru.sentence()
        else:
            Comment = 'NULL'
        ad_dict.append(
            [AddressID, NP_BuyerID, LP_BuyerID, SupplierID, IsRegistered, IsActual, Country, Region, City, Street,
             BuildingNo, Postcode, Comment])
    return ad_dict
# writeXLS('addresses', Addresses(211))

# ///////////// 90 /////////////
def ContactPersons(_range):
    cp_dict = []
    LP_rand = (randomChoice(150, _range))
    SP_rand = (randomChoice(100, _range))
    for i in range(1, _range):
        ContactPersonID = i
        if i % 2 == 0:
            LP_BuyerID = 'NULL'
            SupplierID = SP_rand[i]
        else:
            LP_BuyerID = LP_rand[i]
            SupplierID = 'NULL'
        FullName = fake_ru.name()
        Surname = (FullName.split(' '))[0]
        Name = (FullName.split(' '))[1]
        MiddleName = (FullName.split(' '))[2]
        Position = fake_ru.job()
        Phone = '+7 ' + f'({random.randint(100, 999)})' + ' ' + f'{random.randint(100, 999)}' + '-' + f'{random.randint(10, 99)}' + '-' + f'{random.randint(10, 99)}'
        Email = fake.sentence().split(' ')[1] + f'{math.floor(10000 * math.acosh(i)) + random.randint(1,1000)}' + f'{random.choice(Mails)}'
        if TrueOrFalse(25) == 1:
            Notes = fake_ru.sentence()
        else:
            Notes = 'NULL'
        cp_dict.append(
            [ContactPersonID, LP_BuyerID, SupplierID, Surname, Name, MiddleName, Position, Phone, Email, Notes])
    return cp_dict
# writeXLS('contact-persons', ContactPersons(91))


# ///////////// 30 /////////////
def TareSuppliers(_range):
    ts_dict = []
    for i in range(1, _range):
        TareSupplierID = i
        SupplierID = random.randint(1, 100)
        PackagingID = random.randint(1, 7)
        ts_dict.append([TareSupplierID, SupplierID, PackagingID])
    return ts_dict
# writeXLS('tare-suppliers', TareSuppliers(31))


# ///////////// 1500 /////////////
def Color(_range):
    c_dict = []
    for i in range(1, _range):
        ColorID = i
        CatalogID = random.randint(1, 10)
        ArticleNumber = f'{(catalogs[math.floor(i/(_range * 10))][0:3])}' + f'{fake.ean(length=8)}'
        if TrueOrFalse(25) == 1:
            Description = fake_ru.color_name()
        else:
            Description = 'NULL'
        c_dict.append([ColorID, CatalogID, ArticleNumber, Description])
    return c_dict
# writeXLS('colors', Color(1501))


# ///////////// 100 /////////////
def ProducibleMaterials(_range):
    pm_dict = []
    for i in range(1, _range):
        MaterialID = i
        ProductGroupID = random.randint(1, 10)
        MaterialName = f'Материал№{i}'
        ArticleNumber = f'ЛКМ{fake.ean(length=8)}'
        TypeOfWorks = random.randint(1, 3)
        ExpenditurePer1SquareMetre = random.randint(1, 12)
        PaintDensity = random.randint(50, 200)
        HasASmell = TrueOrFalse(20)
        IsQuickDrying = TrueOrFalse(20)
        ChemicalResistance = random.randint(1, 12)
        MinimumPaintTemperatureCelsius = random.randint(-30, 25)
        IsWeatherproof = TrueOrFalse(20)
        GlossLevel = random.randint(1, 10)
        CSR = fake_ru.bic()
        pm_dict.append([MaterialID, ProductGroupID, MaterialName, ArticleNumber, TypeOfWorks,
                        ExpenditurePer1SquareMetre, PaintDensity, HasASmell, IsQuickDrying, ChemicalResistance,
                        MinimumPaintTemperatureCelsius, IsWeatherproof, GlossLevel, CSR])
    return pm_dict
# writeXLS('producible-materials', ProducibleMaterials(101))


# ///////////// 1500 /////////////
def MaterialObjects(_range):
    mo_dict = []
    for i in range(1,_range):
        recordID = i
        MaterialID = random.randint(1, 100)
        ObjectTypeID = random.randint(1, 14)
        mo_dict.append([recordID, MaterialID, ObjectTypeID])
    return mo_dict
# writeXLS('material-object', MaterialObjects(1501))

# ///////////// 1000 /////////////
def MaterialSurfaces(_range):
    ms_dict = []
    for i in range(1, _range):
        recordID = i
        MaterialID = random.randint(1, 100)
        SurfaceID  = random.randint(1, 10)
        DryingTimeOf1LayerInHours = float(str(random.uniform(0.5, 5.0))[0:3])
        ms_dict.append([recordID, MaterialID, SurfaceID, DryingTimeOf1LayerInHours])
    return ms_dict
# writeXLS('material-surface', MaterialSurfaces(1001))

# ///////////// 250 /////////////
def MaterialtheDyeingMethods(_range):
    mdm_dict = []
    for i in range(1, _range):
        recordID = i
        MaterialID = random.randint(1, 100)
        DyeingMethodID = random.randint(1, 3)
        if TrueOrFalse(25) == 1:
            Recommendations = 'Подробнее о способе нанесения читайте на нашем сайте! --site-lkm.ru--'
        else:
            Recommendations = 'NULL'
        mdm_dict.append([recordID, MaterialID, DyeingMethodID, Recommendations])
    return mdm_dict
# writeXLS('material-dyeingmethod', MaterialtheDyeingMethods(251))


# ///////////// 200 /////////////
def RawMaterials(_range):
    mdm_dict = []
    for i in range(1, _range):
        RawMaterialID  = i
        RawMaterialTypeID = random.randint(1, 10)
        RawMaterialName = fake_ru.sentence()
        mdm_dict.append([RawMaterialID, RawMaterialTypeID, RawMaterialName])
    return mdm_dict
# writeXLS('raw-materials', RawMaterials(201))

# ///////////// 500 /////////////
def MaterialConsistency(_range):
    mc_dict = []
    for i in range(1, _range):
        recordID = i
        MaterialID = random.randint(1, 100)
        RawMaterialID = random.randint(1, 200)
        PercentageInTheComposition = float(str(random.uniform(0.5, 95.0))[0:3])
        if fake.boolean(chance_of_getting_true=25) == 1:
            Notes = fake_ru.sentence()
        else:
            Notes = 'NULL'
        mc_dict.append([recordID, MaterialID, RawMaterialID, PercentageInTheComposition, Notes])
    return mc_dict
# writeXLS('material-consistency', MaterialConsistency(501))


# ///////////// 30 /////////////
measures = ['шт.', 'кг', 'л']
def RawSuppliers(_range):
    rs_dict = []
    for i in range(1, _range):
        recordID = i
        RawSupplierID  = random.randint(1, 50)
        RawMaterialID = random.randint(1, 200)
        RawMaterialUnitOfMeasure = random.choice(measures)
        RawMaterialQuantity = 100 * math.floor(random.randint(20, 10000)/100)
        RawMaterialUnitPrice = 100 * math.floor(random.randint(20, 5000)/100)
        rs_dict.append([recordID, RawSupplierID, RawMaterialID, RawMaterialUnitOfMeasure, RawMaterialQuantity, RawMaterialUnitPrice])
    return rs_dict
# writeXLS('raw-suppliers', RawSuppliers(31))


# ///////////// 5000 /////////////
def PricingPerMadeMaterial(_range):
    ppmm_dict = []
    for i in range(1, _range):
        PriceID  = i
        MaterialID = random.randint(1, 100)
        PackagingID = random.randint(1, 7)
        ColorID = random.randint(1, 1500)
        TotalCost = 'NULL'
        ppmm_dict.append([PriceID, MaterialID, PackagingID, ColorID, TotalCost])
    return ppmm_dict
# writeXLS('pricing-per-made-material', PricingPerMadeMaterial(5001))


# ///////////// 2000 /////////////
def Orders(_range):
    or_dict = []
    for i in range(1, _range):
        OrderID  = i
        BuyerID = random.randint(1, 1000)
        TransportCompanyID  = random.randint(1, 3)
        DeliveryCost = 100 * math.floor(random.randint(20, 20000)/100)
        IsPickUp = TrueOrFalse(20)
        IsCompleted = TrueOrFalse(50)
        OrderDT = fake.date()
        if TrueOrFalse(25) == 1:
            Notes = f'Доставить через {random.randint(5, 10)} дней в {fake_ru.city_name()}'
        else:
            Notes = 'NULL'
        or_dict.append([OrderID, BuyerID, TransportCompanyID, DeliveryCost, IsPickUp, IsCompleted, OrderDT, Notes])
    return or_dict
# writeXLS('orders', Orders(2001))


# ///////////// 5000 /////////////
def OrderItems(_range):
    oi_dict = []
    for i in range(1, _range):
        OrderItemID = i
        OrderID = random.randint(1, 2000)
        PriceID = random.randint(1, 5000)
        Quantity = random.randint(1, 200)
        TotalCost = 'NULL'
        oi_dict.append([OrderItemID, OrderID, PriceID, Quantity, TotalCost])
    return oi_dict
# writeXLS('order-items', OrderItems(5001))


# ///////////// 3000 /////////////
def Shifts(_range):
    sh_dict = []
    j = 1
    for i in range(1, _range):
        StartDT = fake_ru.date()
        EndDT = fake_ru.date()
        while len(sh_dict) < _range:
            try:
                if dateDiff(StartDT, EndDT) > 0:
                    sh_dict.append([j, StartDT, EndDT])
                    j += 1
                else:
                    pass
            except:
                pass
    return sh_dict
# writeXLS('shifts', Shifts(3000))


# ///////////// 2500 /////////////
def InvoicesForPayment(_range):
    ifp_dict = []
    for i in range(1, _range):
        InvoiceID = i
        InvoiceNo = fake_ru.ssn()
        OrderID = random.randint(1, 2000)
        EmployeeID = random.randint(1, 18)
        TotalCost = 'NULL'
        Paid = 'NULL'
        IsFullyPaid = 'NULL'
        ifp_dict.append([InvoiceID, InvoiceNo, OrderID, EmployeeID, TotalCost,
                         Paid, IsFullyPaid])
    return ifp_dict
# writeXLS('invoices-for-payment', InvoicesForPayment(2501))


# ///////////// 6000 /////////////
def WorkingDaysChronicle(_range):
    wdc_dict = []
    for i in range(1, _range):
        recordID  = i
        ShiftID = random.randint(1, 3000)
        EmployeeID = random.randint(1, 18)
        wdc_dict.append([recordID, ShiftID, EmployeeID])
    return wdc_dict
# writeXLS('working-days-chronicle', WorkingDaysChronicle(6001))


# ///////////// 5000 /////////////
def InventoryOfPackagingAndRawMaterials(_range):
    inv_dict = []
    for i in range(1, _range):
        InventoryRecordID   = i
        ShiftID = random.randint(1, 3000)
        RawMaterialID = random.randint(1, 200)
        PackagingID = random.randint(1, 7)
        UnitOfMeasure = random.choice(measures)
        Quantity = 100 * math.floor(random.randint(20, 10000)/100)
        inv_dict.append([InventoryRecordID, ShiftID, RawMaterialID, PackagingID, UnitOfMeasure, Quantity])
    return inv_dict
# writeXLS('inventory-of-packaging', InventoryOfPackagingAndRawMaterials(5001))


# ///////////// 5000 /////////////
def Shipments(_range):
    sh_dict = []
    for i in range(1, _range):
        ShipmentID = i
        InvoiceID = random.randint(1, 2500)
        ShipmentDT = fake.date()
        IsPartial = 'NULL'
        sh_dict.append([ShipmentID, InvoiceID, ShipmentDT, IsPartial])
    return sh_dict
# writeXLS('shipments', Shipments(5001))


# ///////////// 5000 /////////////
def Implementation(_range):
    ip_dict = []
    for i in range(1, _range):
        ConsignmentID = i
        OrderItemID = random.randint(1, 5000)
        ApparatusID = random.randint(1, 7)
        ShiftID = random.randint(1, 3000)
        ShipmentID = random.randint(1, 5000)
        MadeKG = 'NULL'
        RemainsKG = 'NULL'
        ip_dict.append([ConsignmentID, OrderItemID, ApparatusID, ShiftID, ShipmentID, MadeKG, RemainsKG])
    return ip_dict
# writeXLS('implementation', Implementation(5001))

