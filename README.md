![DigiKey Scraper Featured Image](https://raw.githubusercontent.com/omkarcloud/digikey-scraper/master/digikey-scraper-featured-image.png)

# DigiKey Scraper API

REST API to search electronic components and get detailed part specifications, tiered pricing, stock levels, and datasheets from DigiKey. Real-time data, structured JSON.

## Key Features

- Search DigiKey's full electronic components catalog by keyword or part number
- Get 30+ data points per component (specs, pricing tiers, stock, datasheets, lifecycle status)
- Full parametric specifications, quantity-break pricing, and RoHS compliance
- **5,000 requests/month on free tier**
- Example Response:
```json
{
  "digikey_part_number": "497-STM32F407VGT6-ND",
  "manufacturer_part_number": "STM32F407VGT6",
  "manufacturer": "STMicroelectronics",
  "description": "IC MCU 32BIT 1MB FLASH 100LQFP",
  "category": "Microcontrollers - MCU",
  "unit_price": 14.22,
  "currency": "USD",
  "quantity_available": 12540,
  "product_status": "Active",
  "datasheet_url": "https://www.st.com/resource/en/datasheet/stm32f407vg.pdf",
  "rohs_status": "ROHS3 Compliant"
}
```

## Get API Key

Create an account at [omkar.cloud](https://www.omkar.cloud/auth/sign-up?redirect=/api-key) to get your API key.

It takes just 2 minutes to sign up. You get 5,000 free requests every month — more than enough to build a working integration without paying a dime.

This is a well built product, and your search for the best DigiKey Scraper API ends right here.


## Quick Start

```bash
curl -X GET "https://digikey-scraper.omkar.cloud/digikey/search?search_term=STM32F4" \
  -H "API-Key: YOUR_API_KEY"
```

```json
{
  "total_results": 847,
  "components": [
    {
      "digikey_part_number": "497-STM32F407VGT6-ND",
      "manufacturer_part_number": "STM32F407VGT6",
      "manufacturer": "STMicroelectronics",
      "description": "IC MCU 32BIT 1MB FLASH 100LQFP",
      "category": "Microcontrollers - MCU",
      "unit_price": 14.22,
      "currency": "USD",
      "quantity_available": 12540,
      "product_status": "Active",
      "rohs_status": "ROHS3 Compliant"
    }
  ]
}
```

## Quick Start (Python)

```bash
pip install requests
```

```python
import requests

# Search for components
response = requests.get(
    "https://digikey-scraper.omkar.cloud/digikey/search",
    params={"search_term": "STM32F4"},
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```


## API Reference

### Search Components

```
GET https://digikey-scraper.omkar.cloud/digikey/search
```

#### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `search_term` | Yes | — | Keyword, part number fragment, or description to search. |
| `page` | No | `1` | Page number. |

#### Example

```python
import requests

response = requests.get(
    "https://digikey-scraper.omkar.cloud/digikey/search",
    params={"search_term": "STM32F4", "page": 1},
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```

#### Response

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "total_results": 847,
  "components": [
    {
      "digikey_part_number": "497-STM32F407VGT6-ND",
      "manufacturer_part_number": "STM32F407VGT6",
      "manufacturer": "STMicroelectronics",
      "description": "IC MCU 32BIT 1MB FLASH 100LQFP",
      "category": "Microcontrollers - MCU",
      "unit_price": 14.22,
      "currency": "USD",
      "quantity_available": 12540,
      "minimum_order_qty": 1,
      "packaging": "Tray",
      "product_status": "Active",
      "series": "STM32F4",
      "datasheet_url": "https://www.st.com/resource/en/datasheet/stm32f407vg.pdf",
      "product_url": "https://www.digikey.com/en/products/detail/stmicroelectronics/STM32F407VGT6/3356702",
      "thumbnail": "https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2822/497~STM32F407VGT6~100-LQFP.jpg",
      "rohs_status": "ROHS3 Compliant"
    }
  ]
}
```

</details>

---

### Product Details

```
GET https://digikey-scraper.omkar.cloud/digikey/product
```

#### Parameters

| Parameter | Required | Default | Description |
|-----------|----------|---------|-------------|
| `product_id` | Yes | — | DigiKey part number or manufacturer part number (e.g., `LM7805CT-ND`). |

#### Example

```python
import requests

response = requests.get(
    "https://digikey-scraper.omkar.cloud/digikey/product",
    params={"product_id": "LM7805CT-ND"},
    headers={"API-Key": "YOUR_API_KEY"}
)

print(response.json())
```

#### Response Fields

Returns 30+ fields including description, full parametric specifications, quantity-break pricing tiers, real-time stock availability, lead time, datasheet and reference manual links, RoHS compliance, moisture sensitivity level, and product images.

<details>
<summary>Sample Response (click to expand)</summary>

```json
{
  "digikey_part_number": "497-STM32F407VGT6-ND",
  "manufacturer_part_number": "STM32F407VGT6",
  "manufacturer": "STMicroelectronics",
  "description": "IC MCU 32BIT 1MB FLASH 100LQFP",
  "detailed_description": "ARM Cortex-M4 STM32F4 Microcontroller IC 32-Bit Single-Core 168MHz 1MB (1M x 8) FLASH 100-LQFP (14x14)",
  "product_url": "https://www.digikey.com/en/products/detail/stmicroelectronics/STM32F407VGT6/3356702",
  "datasheet_url": "https://www.st.com/resource/en/datasheet/stm32f407vg.pdf",
  "thumbnail": "https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2822/497~STM32F407VGT6~100-LQFP.jpg",
  "images": [
    "https://mm.digikey.com/Volume0/opasdata/d220001/medias/images/2822/497~STM32F407VGT6~100-LQFP.jpg"
  ],
  "category": "Integrated Circuits (ICs)",
  "sub_category": "Microcontrollers - MCU",
  "series": "STM32F4",
  "product_status": "Active",
  "rohs_status": "ROHS3 Compliant",
  "moisture_sensitivity_level": "3 (168 Hours)",
  "packaging": "Tray",
  "quantity_available": 12540,
  "minimum_order_qty": 1,
  "lead_time": "In Stock",
  "pricing": {
    "currency": "USD",
    "tiers": [
      { "break_quantity": 1, "unit_price": 14.22 },
      { "break_quantity": 10, "unit_price": 12.816 },
      { "break_quantity": 25, "unit_price": 12.103 },
      { "break_quantity": 100, "unit_price": 10.276 }
    ]
  },
  "specifications": [
    { "attribute": "Core Processor", "value": "ARM Cortex-M4" },
    { "attribute": "Core Size", "value": "32-Bit Single-Core" },
    { "attribute": "Speed", "value": "168MHz" },
    { "attribute": "Program Memory Size", "value": "1MB (1M x 8)" },
    { "attribute": "Program Memory Type", "value": "FLASH" },
    { "attribute": "RAM Size", "value": "192KB" },
    { "attribute": "Number of I/O", "value": "82" },
    { "attribute": "Voltage - Supply (Vcc/Vdd)", "value": "1.8V ~ 3.6V" },
    { "attribute": "Data Converters", "value": "A/D 16x12b; D/A 2x12b" },
    { "attribute": "Oscillator Type", "value": "Internal" },
    { "attribute": "Operating Temperature", "value": "-40C ~ 85C (TA)" },
    { "attribute": "Package / Case", "value": "100-LQFP" },
    { "attribute": "Connectivity", "value": "CANbus, I2C, IrDA, LINbus, SPI, UART/USART, USB OTG" },
    { "attribute": "Peripherals", "value": "DMA, Motor Control PWM, PDR, POR, PVD, PWM, Temp Sensor, WDT" }
  ],
  "associated_documents": [
    {
      "label": "Datasheet",
      "url": "https://www.st.com/resource/en/datasheet/stm32f407vg.pdf"
    },
    {
      "label": "Reference Manual",
      "url": "https://www.st.com/resource/en/reference_manual/rm0090.pdf"
    }
  ],
  "supplier_device_package": "100-LQFP (14x14)"
}
```

</details>

## Error Handling

```python
response = requests.get(
    "https://digikey-scraper.omkar.cloud/digikey/search",
    params={"search_term": "STM32F4"},
    headers={"API-Key": "YOUR_API_KEY"}
)

if response.status_code == 200:
    data = response.json()
elif response.status_code == 401:
    # Invalid API key
    pass
elif response.status_code == 429:
    # Rate limit exceeded
    pass
```

## FAQs

### What data does the API return?

**Search Components** returns per component: DigiKey part number, manufacturer part number, manufacturer name, description, category, unit price, currency, quantity available, minimum order quantity, packaging type, product status (Active/Obsolete), series, datasheet URL, product page URL, thumbnail, and RoHS compliance status.

**Product Details** returns 30+ fields — full and detailed description, all product images, category and sub-category classification, complete parametric specifications (processor, speed, memory, voltage, I/O, package, etc.), quantity-break pricing tiers, real-time stock availability and lead time, datasheet and reference manual links, RoHS status, moisture sensitivity level, and packaging info.

All in structured JSON. Ready to drop into your BOM tool, procurement pipeline, or inventory system.

### How accurate is the data?

Data is pulled from DigiKey in real time. Every API call fetches live data — not cached or stale results. Prices, stock levels, lead times, and specifications reflect what's on DigiKey right now.

### Can I search by manufacturer part number or DigiKey part number?

Both. Pass either a DigiKey part number (e.g., `497-STM32F407VGT6-ND`) or a manufacturer part number (e.g., `STM32F407VGT6`) to the `product_id` parameter. The Search endpoint also accepts partial part numbers, keywords, or descriptions.

### Does the API return quantity-break pricing?

Yes. The Product Details endpoint returns full tiered pricing — every quantity break and its unit price. Perfect for BOM cost estimation at different production volumes.

### Do I need to handle proxies or CAPTCHAs?

No. The API handles all of that. You make a simple GET request and get clean JSON back. No proxy rotation, no CAPTCHA solving, no HTML parsing.

## Rate Limits

| Plan | Price | Requests/Month |
|------|-------|----------------|
| Free | $0 | 5,000 |
| Starter | $25 | 100,000 |
| Grow | $75 | 1,000,000 |
| Scale | $150 | 10,000,000 |

## Questions? We have answers.

Reach out anytime. We will solve your query within 1 working day.

[![Contact Us on WhatsApp about DigiKey Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/whatsapp-us.png)](https://api.whatsapp.com/send?phone=918178804274&text=I%20have%20a%20question%20about%20the%20DigiKey%20Scraper%20API.)

[![Contact Us on Email about DigiKey Scraper](https://raw.githubusercontent.com/omkarcloud/assets/master/images/ask-on-email.png)](mailto:happy.to.help@omkar.cloud?subject=DigiKey%20Scraper%20API%20Question)
