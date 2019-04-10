# 企贷申请创建
## 描述
支持企业申请创建。申请创建成功后，需要保存响应参数中的“申请ID”，作为后续交易的请求参数。

## API代码
loan_app:cp_app:create

## 示例代码
具体方法详见<a href="https://codeload.github.com/lianjintai/openapi-demo-java/zip/master" target="_blank">接口demo下载</a>,包路径[com.ljt.openapi.demo.demos.loanAppCpAppCreateDemo]

## 请求参数

全部需求提供的数据结构：

    1. 企业信息 
       - 客户信息
       - 工商税务信息
       - 经营许可证信息
       - 特色信息（自定义字段）
    2. 经营信息 
    3. 企业财报
    4. 主要成员
       - 关联信息
       - 身份信息
       - 财务信息
       - 经营/职业信息
    5. 联系人信息
    6. 业务信息
    7. 定性打分信息
    8. 申请材料信息
    
具体定义如下：<br>

| 名称 | 类型 | 是否必须 | 描述 | 
| --- | --- | --- | --- |
| cif | JSON | 是 | 企业信息 见[企业信息](#企业信息) | 
| biz | JSON | 否 | 经营信息 | 
| fin | JSON | 否 | 企业财报 见[企业财报信息](#企业财报信息) | 
| rel | JSON | 否 | 主要成员 有且只有一个 见[主要成员](#企业主要成员) | 
| contact | JSON(List) | 否 | 联系人信息，可录入多个，但至少有一个 | 
| fac | JSON | 是 | 业务信息  | 
| doc | JSON | 否 | 申请材料信息 见[申请材料](#企业申请材料) | 
| ccms | JSON | 否 | 定性打分 见[定性打分](#定性打分信息) | 
| callbackURL | String | 否 | 授信状态变更后通知回调URL( 如:http://api.xxxx.com/ljt/callback )，见[授信状态变更通知回调](/2.1/07_app_sts_call_back.md) | |

### 企业信息
企业借款人信息由四部分组成

| 名称 | 类型 | 是否必须 | 描述 | 
| --- | --- | --- | --- | 
| corporate | JSON | 是 | 客户信息 |
| taxInfo | JSON | 否 | 工商税务信息|
| bizCertificates | JSON（list） | 否 | 经营许可证信息 | 
| feature | JSON | 否 | 特色信息 ||


### 企业财报信息
企业财报信息由以下信息组成
财报模版
<a href="https://dcms.lianjintai.com/downloads/finance/%E7%B3%BB%E7%BB%9F07%E7%89%88%E4%BC%81%E4%B8%9A%E8%B4%A2%E5%8A%A1%E6%8A%A5%E8%A1%A8.xlsx" target="_blank">07版财报模版</a>,
<a href="https://dcms.lianjintai.com/downloads/finance/%E7%B3%BB%E7%BB%9F05%E7%89%88%E4%BC%81%E4%B8%9A%E8%B4%A2%E5%8A%A1%E6%8A%A5%E8%A1%A8.xlsx" target="_blank">05版财报模版</a>

注：明细代码“BS88”值需要根据《<a href="https://dcms.lianjintai.com/static/downloads/finance/%E7%B3%BB%E7%BB%9F07%E7%89%88%E4%BC%81%E4%B8%9A%E8%B4%A2%E5%8A%A1%E6%8A%A5%E8%A1%A8.xlsx" target="_blank">07版财报模版</a>》或者《<a href="https://dcms.lianjintai.com/static/downloads/finance/%E7%B3%BB%E7%BB%9F05%E7%89%88%E4%BC%81%E4%B8%9A%E8%B4%A2%E5%8A%A1%E6%8A%A5%E8%A1%A8.xlsx" target="_blank">05版财报模版</a>》中的公式计算得出，此值影响是否生成企业评分

#### 企业财报请求参数
| 名称 | 类型 | 是否必须 | 描述 | 示例值 | 
| --- | --- | --- | --- | --- |
| mtFinFmtCd | String | 是 | 财务报表格式代码（000-05版财报、004-07版财报） | 004 | 
| mtFinRptCatCd | String | 是 | 财务报表范围代码（1-本部报表、2-合并报表） | 1 | 
| mtFinRptTypCd | String | 是 | 财务报表类型代码（1-年报、2-季报、3-月报、4-半年报） | 1 | 
| mtFinStsCd | String | 是 | 财务报表状态代码（001-已审计、002-未审计） | 001 | 
| dtFin | Date | 是 | 财务报表截止日期（财务报表类型对应范围内的任意日期） | 2017-05-03 | 
| finItems | JSON(Map) | 是 | 财务报表明细， 具体详见[财务报表明细](#财务报表明细) | | |

#### 财务报表明细

| 名称 | 类型 | 是否必须 | 最大长度 | 描述 | 示例值 | 
| --- | --- | --- | --- | --- | --- |
| key | String | 是 | 20 | 财务报表明细代码（根据财务报表格式代码从不同的财报模版中获取，公式列为空且非标题行的代码值） | ANNEX02 | 
| value | Number | 是 | 30(26,4) | 财务报表明细金额（获取代码cd所对应的金额） | 30520.13 | |

### 企业主要成员
企业主要成员信息由以下信息组成

| 名称 | 类型 | 是否必须 | 描述 |  
| --- | --- | --- | --- | 
| legalRelInfo | JSON | 是 | 关联信息| 
| identity | JSON | 是 | 身份信息| 
| finance | JSON | 是 | 财务信息| 
| emplymt | JSON | 是 | 经营/职业信息| |


### 申请材料
| 名称 | 类型 | 是否必须  | 描述 | 
| --- | --- | --- | ---  |
| cifDocRefId | string | 否 | 从获取产品配置API中返回的"doc.docs[].refId"值,但要求"mtDocTypeCd=CIF" | 
| facDocRefId | string | 否 | 从获取产品配置API中返回的"doc.docs[].refId"值,但要求“mtDocTypeCd=FAC”  | |


### 定性打分信息
参数数据从[企业获取定性评分](06_cp_credit_model.md)中获取

| 名称 | 类型 | 是否必须 | 最大长度 | 描述 | 
| --- | --- | --- | --- | --- | 
| mtCpCreditModelCd | String | 是 |  | 企业指标模型cd,[企业获取定性评分](06_cp_credit_model.md)API返回的“mtCpCreditModelCd”值 |
| options | JSON(list) | 是 |  | 企业指标模型选项 [定性打分项](#定性打分项) | |

#### 定性打分项

| 名称 | 类型 | 是否必须 | 最大长度 | 描述 |  示例 | 
| --- | --- | --- | --- | --- | --- |
| cd | String | 是 |  | 企业指标评分项cd,[企业获取定性评分](06_cp_credit_model.md)API返回的“mtCpCreditModelIndexList[].cd”值 |  zczj |
| selected | JSON(list) | 是 |  | 企业指标评分项选择cd，,[企业获取定性评分](06_cp_credit_model.md)API返回的“mtCpCreditModelIndexList[].options[].cd”值 | ["A","B"] ||


## 响应参数
| 名称 | 类型 | 描述 |示例值 |
| --- | --- | --- | --- |
| app_id | String | 申请ID | 0092728480d24f5d87bf63639b5cfe1c |

## 错误码
| 描述 | HTTP状态码 | 语义 |
| --- | --- | --- | 
| app_id未找到 | 400 | 请输入正确的app_id,或检查申请类型与申请ID是否匹配 |
| 存在在途申请 | 405 | 客户的前一笔融资请求尚未批准或取消，无法再次发起新融资申请 |


## 请求参数示例

### 请求示例_完整参数_关联人为私营业主 
```javascript

  {
    "cif": {
      "corporate": {
        "mtCifCatCd": "111",
        "mtCorpSalutationCd": "1",
        "mtFinInsttnCd": "01",
        "nationalityMtCtryCd": "CN",
        "mtIndCd": "c305",
        "isComb": "N",
        "mtListedCd": "Y",
        "isFreeTradeArea": "Y",
        "cancelledNum": 0,
        "approvedNum": 0,
        "nm": "测试借款企业7",
        "idNo": "450273020039113424",
        "mtCifIdTypCd": "C2",
        "coreBiz": "测试",
        "principalNo": "136677889",
        "mtCtryCd": "CN",
        "mtStateCd": "110000",
        "mtCityCd": "110100",
        "brandNm": "12",
        "grpNm": "12121212121",
        "website": "www.baidu.com",
        "mtIndCatCd": "c30",
        "mtIndDetailCd": "c3055",
        "mtIndTypCd": "c",
        "stockCode": "123456"
      },
      "taxInfo": {
        "dtRegistered": "2018-10-26 00:00:00",
        "bizRegDtExpiry": "",
        "authCapital": "12",
        "registeredAddr": "12",
        "isBussLongEffec": "Y",
        "incomeTaxNo": "00000000",
        "nationalTaxNo": "88888888",
        "corpIdNo": "3212313215468798"
      },
      "bizCertificates": [
        {
          "mtBizCertificateTypCd": "00",
          "no": "123213213213",
          "dtExpiry": "2020-07-14 00:00:00"
        },
        {
          "mtBizCertificateTypCd": "00",
          "no": "888888888888888",
          "dtExpiry": "2020-07-14 00:00:00"
        }
      ]
    },
    "biz": {
      "employeeCnt": "1",
      "assetAmt": "1",
      "noOfBizSite": 1,
      "mtCorpTypeCd": "04",
      "dtCommenceTrading": "2018-10-30 00:00:00",
      "bizAddr": "1",
      "mtBizLandOwnerCd": "1",
      "bizLandArea": 1,
      "saleAmt": "1",
      "ratal": "1",
      "waterDosage": "1",
      "electricityDosage": "1",
      "salaryTotal": "1",
      "mtSalaryTypCd": "1",
      "socialSecurity": "1",
      "equityLine": "1"
    },
   "fin": {
      "mtFinFmtCd": "004",
      "mtFinRptCatCd": "1",
      "mtFinRptTypCd": "1",
      "mtFinStsCd": "001",
      "dtFin": "2017-05-03",
      "finItems": {
        "BS88": "0",
        "ANNEX026": "1419144.7",
        "ANNEX08": "13487368.34",
        "ANNEX09": "6438224.76",
        "ANNEX10": "9700377.53",
        "ANNEX11": "35561095.45",
        "ANNEX12": "40264711.04",
        "ANNEX13": "13794328.73"
      }
    },
    "rel": {
      "legalRelInfo": {
        "isActualCtrl": "Y",
        "isInvolvedMgmt": "Y",
        "dtInCompSince": "2016-06-27 00:00:00",
        "dtInBizLineSince": "2016-06-27 00:00:00",
        "mgmtExperience": "dddd",
        "mtPosHeldCd": "001"
      },
      "identity": {
        "mtCifIdTypCd": "I2",
        "idNo": "ddfdsfds",
        "isLongEffec": "N",
        "dtExpiry": "",
        "nationalityMtCtryCd": "CN",
        "nm": "dddd",
        "mtGenderCd": "M",
        "mtMaritalStsCd": "02",
        "dtRegistered": "2018-11-01 00:00:00",
        "mtCityCd": "110100",
        "mtCtryCd": "CN",
        "mtStateCd": "110000",
        "mtResidenceStsCd": "01",
        "mobileNo": "13887597721",
        "mtIndvMobileUsageStsCd": "03",
        "mtEduLvlCd": "02",
        "email": "912933515@qq.com",
        "weChat": "13887597721",
        "qq": "912933515"
      },
      "finance": {
        "hasCar": "Y",
        "hasCreditCard": "Y",
        "isFamily": "Y",
        "yearIncAmt": "12321",
        "plateNo": "1",
        "creditCardLines": "1"
      },
      "emplymt": {
        "isComb": "Y",
        "bizRegDtExpiry": "",
        "isLeglaRep": "",
        "isBussLongEffec": "Y",
        "bizRegNo": "817004118277404585",
        "bizAddr": "经营地址",
        "isLegalRep": "Y",
        "currentTotal": "12",
        "yearSaleMarginsRate": "12",
        "ratal": "13",
        "electricityDosage": "14",
        "waterDosage": "15",
        "socialSecurity": "16",
        "equityLine": "17",
        "employees": "18",
        "salaryTotal": "29",
        "workPhone": "联系电话",
        "mtIndDetailCd": "c2412",
        "mtIndCatCd": "c24",
        "mtIndCd": "c241",
        "mtIndTypCd": "c",
        "bizArea": "经营范围",
        "isBizEntity": "Y"
      }
    },
    "contact": [
      {
        "nm": "测试的联系人",
        "mobileNo": "15811269699",
        "mtPosHeldCd": "005",
        "email": "89asdsa@qq.com"
      },
      {
        "nm": "测试的联系人2",
        "mobileNo": "15811269888",
        "mtPosHeldCd": "005",
        "email": "biany@lianjintai.com"
      }
    ],
    "fac": {
      "mtFacCd": "1026",
      "lmtAppr": "12",
      "isRevolvingAllowed": "Y",
      "mtTimeCd": "M",
      "tenureAppr": "12",
      "mtFacTypCd": "1",
      "intRate": "12",
      "intRateInSuspense": "12",
      "mtRepymtTypCd": "005",
      "mtFacPurCdList": [
        {
          "mtFacPurCd": "1001"
        }
      ],
      "deductAcctNo": "6039425988",
      "mtIntRateTypCd": "Y"
    },
    "doc": {
      "cifDocRefId": "bee503b47798415bb19382ab68aba1f1",
      "facDocRefId": "d317f08e5eb442738ebc9f82efd3c121"
    },
    "ccms": {
      "mtCpCreditModelCd": "N1",
      "options": [
        {
          "selected": [
            "A"
          ],
          "cd": "chhfw"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "cwgl"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "gdzcld"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "gjzc"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "dfzc"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "hytzhj"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "qybj"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "ssxfsc"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "yjnl"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "ywgc"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "yysr"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "zczj"
        }
      ]
    },
    "callbackURL": "http://www.xxx.com/xxx/xxx"
  }

```
### 请求示例 完整参数 关联人为非私营业主
```javascript
  {
    "cif": {
      "corporate": {
        "mtCifCatCd": "111",
        "mtCorpSalutationCd": "1",
        "mtFinInsttnCd": "01",
        "nationalityMtCtryCd": "CN",
        "mtIndCd": "c305",
        "isComb": "N",
        "mtListedCd": "Y",
        "isFreeTradeArea": "Y",
        "cancelledNum": 0,
        "approvedNum": 0,
        "nm": "测试借款企业7",
        "idNo": "450273020039113424",
        "mtCifIdTypCd": "C2",
        "coreBiz": "测试",
        "principalNo": "136677889",
        "mtCtryCd": "CN",
        "mtStateCd": "110000",
        "mtCityCd": "110100",
        "brandNm": "12",
        "grpNm": "12121212121",
        "website": "www.baidu.com",
        "mtIndCatCd": "c30",
        "mtIndDetailCd": "c3055",
        "mtIndTypCd": "c",
        "stockCode": "123456"
      },
      "taxInfo": {
        "dtRegistered": "2018-10-26 00:00:00",
        "bizRegDtExpiry": "",
        "authCapital": "12",
        "registeredAddr": "12",
        "isBussLongEffec": "Y",
        "incomeTaxNo": "00000000",
        "nationalTaxNo": "88888888",
        "corpIdNo": "3212313215468798"
      },
      "bizCertificates": [
        {
          "mtBizCertificateTypCd": "00",
          "no": "123213213213",
          "dtExpiry": "2020-07-14 00:00:00"
        },
        {
          "mtBizCertificateTypCd": "00",
          "no": "888888888888888",
          "dtExpiry": "2020-07-14 00:00:00"
        }
      ]
    },
    "biz": {
      "employeeCnt": "1",
      "assetAmt": "1",
      "noOfBizSite": 1,
      "mtCorpTypeCd": "04",
      "dtCommenceTrading": "2018-10-30 00:00:00",
      "bizAddr": "1",
      "mtBizLandOwnerCd": "1",
      "bizLandArea": 1,
      "saleAmt": "1",
      "ratal": "1",
      "waterDosage": "1",
      "electricityDosage": "1",
      "salaryTotal": "1",
      "mtSalaryTypCd": "1",
      "socialSecurity": "1",
      "equityLine": "1"
    },
    "fin": {
      "mtFinFmtCd": "004",
      "mtFinRptCatCd": "1",
      "mtFinRptTypCd": "1",
      "mtFinStsCd": "001",
      "dtFin": "2017-05-03",
      "finItems": {
        "BS88": "0",
        "ANNEX026": "1419144.7",
        "ANNEX08": "13487368.34",
        "ANNEX09": "6438224.76",
        "ANNEX10": "9700377.53",
        "ANNEX11": "35561095.45",
        "ANNEX12": "40264711.04",
        "ANNEX13": "13794328.73"
      }
    },
    "rel": {
      "legalRelInfo": {
        "isActualCtrl": "Y",
        "isInvolvedMgmt": "Y",
        "dtInCompSince": "2016-06-27 00:00:00",
        "dtInBizLineSince": "2016-06-27 00:00:00",
        "mgmtExperience": "dddd",
        "mtPosHeldCd": "001"
      },
      "identity": {
        "mtCifIdTypCd": "I2",
        "idNo": "ddfdsfds",
        "isLongEffec": "N",
        "dtExpiry": "",
        "nationalityMtCtryCd": "CN",
        "nm": "dddd",
        "mtGenderCd": "M",
        "mtMaritalStsCd": "02",
        "dtRegistered": "2018-11-01 00:00:00",
        "mtCityCd": "110100",
        "mtCtryCd": "CN",
        "mtStateCd": "110000",
        "mtResidenceStsCd": "01",
        "mobileNo": "13887597721",
        "mtIndvMobileUsageStsCd": "03",
        "mtEduLvlCd": "02",
        "email": "912933515@qq.com",
        "weChat": "13887597721",
        "qq": "912933515"
      },
      "finance": {
        "hasCar": "Y",
        "hasCreditCard": "Y",
        "isFamily": "Y",
        "yearIncAmt": "12321",
        "plateNo": "1",
        "creditCardLines": "1"
      },
      "emplymt": {
        "mtJobSectorCd": "30200",
        "dtWorkInCurrIndustry": "2013-06-24 00:00:00",
        "mtPosHeldCd": "005",
        "employerNm": "1111",
        "prevServiceYr": "1",
        "prevServiceMth": "1",
        "employerPhone": "11",
        "isBizEntity": "N"
      }
    },
    "contact": [
      {
        "nm": "测试的联系人",
        "mobileNo": "15811269699",
        "mtPosHeldCd": "005",
        "email": "89asdsa@qq.com"
      },
      {
        "nm": "测试的联系人2",
        "mobileNo": "15811269888",
        "mtPosHeldCd": "005",
        "email": "biany@lianjintai.com"
      }
    ],
    "fac": {
      "mtFacCd": "1026",
      "lmtAppr": "12",
      "isRevolvingAllowed": "Y",
      "mtTimeCd": "M",
      "tenureAppr": "12",
      "mtFacTypCd": "1",
      "intRate": "12",
      "intRateInSuspense": "12",
      "mtRepymtTypCd": "005",
      "mtFacPurCdList": [
        {
          "mtFacPurCd": "1001"
        }
      ],
      "deductAcctNo": "6039425988",
      "mtIntRateTypCd": "Y"
    },
    "doc": {
      "cifDocRefId": "bee503b47798415bb19382ab68aba1f1",
      "facDocRefId": "d317f08e5eb442738ebc9f82efd3c121"
    },
    "ccms": {
      "mtCpCreditModelCd": "N1",
      "options": [
        {
          "selected": [
            "A"
          ],
          "cd": "chhfw"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "cwgl"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "gdzcld"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "gjzc"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "dfzc"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "hytzhj"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "qybj"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "ssxfsc"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "yjnl"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "ywgc"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "yysr"
        },
        {
          "selected": [
            "A"
          ],
          "cd": "zczj"
        }
      ]
    },
    "callbackURL": "http://www.xxx.com/xxx/xxx"
  }
```



## 返回示例（正常）
```javascript
{
    "appId":"0092728480d24f5d87bf63639b5cfe1c"
}
```

## 返回示例（异常）
```javascript
{
  "error": "500",
  "message": "没有获取到用户身份信息",
  "timestamp": "2016-12-29 15:10:32"
}
```


## FAQ
关于此文档暂时还没有FAQ