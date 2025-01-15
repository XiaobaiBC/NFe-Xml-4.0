# XML 制作指导文件

在此指导文件中，我们将详细解释如何根据给定的 XML 结构创建和理解一个电子发票文件。我们将详细说明每个部分的功能及其内容，以确保在创建发票时可以正确理解每个标签的作用。

## 1. 文件头部

XML 文件的开头包含了版本声明和命名空间信息，这些对于 XML 文件的解析至关重要。

```xml
<?xml version="1.0" encoding="UTF-8"?>
<nfeProc xmlns="http://www.portalfiscal.inf.br/nfe" versao="4.00">
```

- `<?xml version="1.0" encoding="UTF-8"?>` 表示 XML 文件的版本和编码方式，通常保持不变。
- `<nfeProc xmlns="http://www.portalfiscal.inf.br/nfe" versao="4.00">` 定义了命名空间，确保文件遵循正确的 XML 标准，以及版本 `4.00`。

## 2. 发票信息 (`infNFe`)

`infNFe` 标签包含了与发票相关的所有基本信息，它是 XML 文件的核心部分。通过理解每个元素的含义，可以确保发票文件的正确生成。

### 2.1 基本信息

```xml
<infNFe versao="4.00" Id="NFe00000000000000000000000000000000000000000000">
    <ide>
        <cUF>35</cUF>
        <cNF>07364721</cNF>
        <natOp>Venda de mercadoria</natOp>
        <mod>55</mod>
        <serie>3</serie>
        <nNF>50</nNF>
        <dhEmi>2024-12-29T16:55:17-03:00</dhEmi>
        <dhSaiEnt>2024-12-29T16:55:17-03:00</dhSaiEnt>
        <tpNF>1</tpNF>
        <idDest>2</idDest>
        <cMunFG>3550308</cMunFG>
        <tpImp>1</tpImp>
        <tpEmis>1</tpEmis>
        <cDV>0</cDV>
        <tpAmb>1</tpAmb>
        <finNFe>1</finNFe>
        <indFinal>1</indFinal>
        <indPres>9</indPres>
        <indIntermed>0</indIntermed>
        <procEmi>0</procEmi>
        <verProc>Bling 1.0</verProc>
    </ide>
</infNFe>
```

- `cUF`: 发票所在的州代码（`35` 表示圣保罗州）。
- `cNF`: 发票的唯一编号。
- `natOp`: 交易的性质，`Venda de mercadoria` 表示商品销售。
- `mod`: 电子发票的类型，`55` 表示电子发票。
- `serie`: 发票的系列号，用于分类。
- `nNF`: 发票的号码。
- `dhEmi` 和 `dhSaiEnt`: 发票开具时间和货物发出时间。
- `tpNF`: 发票类型（`1` 表示销售发票）。
- `idDest`: 目的地指示，`2` 表示跨州交易。

### 2.2 发票发出方 (`emit`)

```xml
<emit>
    <CNPJ>00000000000000</CNPJ>
    <xNome>公司名称</xNome>
    <xFant>公司别名</xFant>
    <enderEmit>
        <xLgr>公司街道名称</xLgr>
        <nro>公司门牌号</nro>
        <xBairro>公司街区名称</xBairro>
        <cMun>3550308</cMun>
        <xMun>Sao Paulo</xMun>
        <UF>SP</UF>
        <CEP>00000-000</CEP>
        <cPais>1058</cPais>
        <xPais>Brasil</xPais>
        <fone>(xxxxxxxxxxx)</fone>
    </enderEmit>
    <IE>000000000000</IE>
    <IM>00000000</IM>
    <CNAE>0000000</CNAE>
    <CRT>3</CRT>
</emit>
```

- `<CNPJ>`: 发票开具方的企业注册号。
- `<xNome>`: 企业的正式名称。
- `<xFant>`: 企业的别名。
- `<enderEmit>`: 企业的地址信息。
- `<IE>`: 纳税人的州登记号（`Inscrição Estadual`）。
- `<CRT>`: 税务注册类型，`3` 表示普通税制。

### 2.3 发票接收方 (`dest`)

```xml
<dest>
    <CNPJ>00000000000000</CNPJ>
    <xNome>购买方名称</xNome>
    <enderDest>
        <xLgr>购买街道名称</xLgr>
        <nro>购买门牌号</nro>
        <xBairro>购买街区名称</xBairro>
        <cMun>购买城市代码</cMun>
        <xMun>购买城市名称</xMun>
        <UF>PR</UF>
        <CEP>00000000</CEP>
        <cPais>1058</cPais>
        <xPais>Brasil</xPais>
        <fone>xxxxxxxxxxx</fone>
    </enderDest>
    <indIEDest>1</indIEDest>
    <IE>0000000000</IE>
</dest>
```

- `<CNPJ>`: 发票接收方的企业注册号。
- `<xNome>`: 发票接收方的名称。
- `<enderDest>`: 发票接收方的地址信息。
- `<indIEDest>`: 表示接收方是否为外国企业（`1` 表示是）。

### 2.4 商品详情 (`det`)

```xml
<det nItem="1">
    <prod>
        <cProd>00000000</cProd>
        <cEAN>SEM GTIN</cEAN>
        <xProd>商品名称</xProd>
        <NCM>商品海关编码</NCM>
        <CFOP>xxxx</CFOP>
        <uCom>PC</uCom>
        <qCom>1.0000</qCom>
        <vUnCom>1824.0000000000</vUnCom>
        <vProd>1824.00</vProd>
    </prod>
    <imposto>
        <vTotTrib>667.14</vTotTrib>
        <ICMS>
            <ICMS00>
                <orig>1</orig>
                <CST>00</CST>
                <modBC>3</modBC>
                <vBC>1824.00</vBC>
                <pICMS>4.0000</pICMS>
                <vICMS>72.96</vICMS>
            </ICMS00>
        </ICMS>
    </imposto>
</det>
```

- `nItem`: 商品的序列号。
- `cProd`: 商品代码。
- `xProd`: 商品名称。
- `NCM`: 商品的海关编码（用于国际贸易）。
- `CFOP`: 商品的税务编码。
- `qCom`: 商品数量。
- `vUnCom`: 单价。
- `vProd`: 总价。

### 2.5 税务信息 (`imposto`)

每个商品项都会包含税务信息，涵盖了增值税（ICMS）、社会贡献（PIS、COFINS）等税种。

- `ICMS`: 增值税，包含税务基础值、税率以及税额。
- `PIS` 和 `COFINS`: 社会贡献税，分别记录了相应的税务信息。

## 3. 发票总计 (`total`)

```xml
<total>
    <ICMSTot>
        <vBC>7590.00</vBC>
        <vICMS>303.60</vICMS>
        <vProd>7590.00</vProd>
        <vFrete>100.00</vFrete>
        <vNF>7690.00</vNF>
        <vTotTrib>2776.09</vTotTrib>
    </ICMSTot>
</total>
```

- `vBC`: 商品的税务基础值。
- `vICMS`: 增值税的总税额。
- `vProd`: 商品总价。
- `vFrete`: 运费。
- `vNF`: 发票总额。

## 4. 支付信息 (`pag`)

```xml
<pag>
    <detPag>
        <indPag>0</indPag>
        <tPag>15</tPag>
        <vPag>7690.00</vPag>
    </detPag>
</pag>
```

- `tPag`: 支付方式（例如，`15` 表示通过信用卡支付）。
- `vPag`: 支付金额。

## 5. 附加信息和技术支持 (`infAdic`, `infRespTec`

)

```xml
<infAdic>
    <infAdFisco>Informações adicionais para o fisco.</infAdFisco>
</infAdic>
<infRespTec>
    <CNPJ>00000000000000</CNPJ>
    <xContato>Suporte Técnico</xContato>
    <email>contato@empresa.com</email>
    <fone>(11) 1234-5678</fone>
</infRespTec>
```

- `infAdic`: 附加信息，可以用于提供额外的备注。
- `infRespTec`: 技术支持信息，通常用于提供系统相关的联系方式。

## 结论

通过理解这些关键字段及其结构，您可以准确地生成符合要求的 NF-e XML 文件。这些字段包含了发票的基本信息、商品详情、税务计算、支付方式等内容，确保了电子发票的完整性与合规性。
