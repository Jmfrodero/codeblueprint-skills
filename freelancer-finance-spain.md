# Freelancer Finance Spain

> Complete financial management system for Spanish freelancers and autónomos.

## Overview

This skill provides a comprehensive framework for managing freelance finances in Spain, covering income tracking, expense categorization, quarterly tax summaries, and AI-assisted document generation for the Spanish tax system.

**Applicable tax regime:** Sistema de Módulos (estimación directa simplificada and estimación directa normal)

---

## 1. Income Tracking

### Monthly Income Log

Maintain a structured monthly record of all income:

```
## INCOME ENTRY
Date: [YYYY-MM-DD]
Client: [Client Name / Nombre del Cliente]
Invoice Number: [Serie-Número]
Gross Amount (Base Imponible): €[amount]
VAT (IVA 21%/10%/4%): €[amount]
Retention (Retención IRPF 15%/7%): -€[amount]
Net Received: €[amount]
Payment Method: [Transfer/Bizum/Cash]
Status: [Pending/Paid]
```

### Income Categories (Categorías de Ingreso)

| Category | Description | IVA Rate | IRPF Retention |
|----------|-------------|----------|----------------|
| Servicios profesionales | Consulting, advisory, freelance services | 21% | 15%* |
| Desarrollo web/software | Web development, programming | 21% | 15%* |
| Diseño gráfico | Graphic design services | 21% | 15%* |
| Formación/Cursos | Training and education | 21% | 15%* |
| Traducción | Translation services | 21% | 15%* |
| Asesoría | Professional advice | 21% | 15%* |
| Comisiones | Commissions and royalties | 21% | 15%* |
| Ventas de productos | Product sales (goods) | 21% | No retention |
| Autoconsumo | Personal use of business assets | 21% | 15%* |

*IRPF retention reduced to 7% for the first 3 years of activity (inicio de actividad).

### Quarterly Income Summary Template

```
## CUATRIMESTRE [Q1/Q2/Q3/Q4] - AÑO [YYYY]

### Resumen de Ingresos
| Concepto | Base Imponible | IVA Repercutido | Total Facturado |
|----------|----------------|-----------------|-----------------|
| Enero    | €X,XXX.XX      | €XXX.XX         | €X,XXX.XX       |
| Febrero  | €X,XXX.XX      | €XXX.XX         | €X,XXX.XX       |
| Marzo    | €X,XXX.XX      | €XXX.XX         | €X,XXX.XX       |
| **TOTAL**| **€X,XXX.XX**  | **€X,XXX.XX**   | **€X,XXX.XX**   |

### Retenciones practicadas (ingresos)
| Mes      | Base Retención | IRPF Retenido |
|----------|----------------|---------------|
| Enero    | €X,XXX.XX      | -€XXX.XX      |
| ...      | ...            | ...           |
| **TOTAL**| **€X,XXX.XX**  | **-€XXX.XX**  |
```

---

## 2. Expense Categories (Categorías de Gastos)

### Deductible Expense Categories

| Category | Examples | Deductible % | Notes |
|----------|---------|--------------|-------|
| **Suministros** | Electricidad, agua, gas, internet del domicilio profesional | % proporcional | Mantén justificante del % uso profesional |
| **Material de oficina** | Papelería, cartuchos tinta, cuadernos | 100% | Factura a nombre del autónomo |
| **Software/SaaS** | Adobe CC, Office 365, hosting, dominios | 100% | Licencias para uso profesional |
| **Equipos informáticos** | Ordenador, móvil, tablet | 100% | Amortización anual (~26% valor compra) |
| **Mobiliario** | Escritorio, silla ergonómica, estanterías | 100% | Amortización (~10% anual) |
| **Comunicación** | Teléfono móvil profesional | 100% (o %) | Separar uso personal y profesional |
| **Desplazamientos** | Combustible, transporte público, peajes | 100% | Con justificantes y motivo profesional |
| **Dietas** | Comidas durante desplazamientos profesionales | €26.83/día (España) | Dentro de límites establecida |
| **Vehículo** | Compra, renting, seguro, mantenimiento | % uso profesional | Libro de flotteo obligatorio |
| **Cotizaciones SS** | Cuota autónomo (RETA) | 100% | Obligatoria desde 01/01/2023: min €230/m |
| **Seguros** | Responsabilidad civil, salud, bajas | 100% | Profesional y/o empresa |
| **Contabilidad** | Gestoría, software contabilidad | 100% | Necesario para estimación directa |
| **Formación** | Cursos, certificaciones, libros | 100% | Relacionados con actividad profesional |
| **Marketing** | Web, publicidad, tarjetas, SEO | 100% | Deducible si orientado a negocio |
| **Impuestos locales** | IAE, cuota cámara comercio | 100% | Tasas y licencias |
| **Alquiler espacio** | Coworking, oficina profesional | 100% | Con contrato y justificantes |
| **Hosting/Dominios** | Servidores, dominios web | 100% | Necesarios para actividad |
| **Plataformas** | Freelance platforms, marketplaces | 100% | Comisiones deducibles |
| **Protección Social** | Complementos pensiones, seguros | 100% | Hasta límites legales |
| **Libros Profesionales** | Publicaciones técnicas, suscripciones | 100% | Vinculados a actividad |

### Non-Deductible Expenses

- Multas de tráfico y sanciones
- Gastos suntuarios (no relacionados con actividad)
- Compra de vivienda (salvo adaptación business)
- IVA de gastos no deducibles (repercutido al gasto)
- Retirada de bénéfices para uso pessoal
- Primas de seguros de salud (sin límite, pero con condiciones)

### Monthly Expense Log

```
## GASTO ENTRY
Date: [YYYY-MM-DD]
Supplier: [Nombre proveedor]
Invoice Number: [Número factura]
Category: [From table above]
Description: [Descripción del gasto]
Base Imponible: €[amount]
IVA Soportado: €[amount]
IRPF Retention: -€[amount] (si aplica)
Total Pagado: €[amount]
Payment Method: [Transfer/Tarjeta/Cash]
Deductible %: [100%/XX%]
```

### Quarterly Expense Summary Template

```
## CUATRIMESTRE [Q1/Q2/Q3/Q4] - AÑO [YYYY]

### Resumen de Gastos Deducibles
| Categoría              | Base Imponible | IVA Soportado | Total Deducible |
|------------------------|----------------|---------------|-----------------|
| Suministros            | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Material oficina       | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Software/SaaS          | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Equipos informáticos   | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Desplazamientos        | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Dietas                 | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Vehículo              | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Cotización SS          | €XXX.XX        | -             | €XXX.XX         |
| Seguros                | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Contabilidad/Gestoría  | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Formación              | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Marketing              | €XXX.XX        | €XX.XX        | €XXX.XX         |
| Otros                  | €XXX.XX        | €XX.XX        | €XXX.XX         |
| **TOTAL**              | **€X,XXX.XX**  | **€XXX.XX**   | **€X,XXX.XX**   |

### IVA Soportado Deducible (resumen)
| Trimestre | IVA Soportado | IVA Deducible | IVA No Deducible |
|-----------|---------------|---------------|------------------|
| IVA Q1    | €XXX.XX       | €XXX.XX       | €XX.XX           |
| IVA Q2    | €XXX.XX       | €XXX.XX       | €XX.XX           |
| IVA Q3    | €XXX.XX       | €XXX.XX       | €XX.XX           |
| IVA Q4    | €XXX.XX       | €XXX.XX       | €XX.XX           |
```

---

## 3. Modelo 303 Quarterly Summary

### Structure of Modelo 303

The **Modelo 303** declares VAT (IVA) quarterly. Use this template:

```
## MODELO 303 - DECLARACIÓN TRIMESTRAL IVA
Período: [01/01-31/03 / 01/04-30/06 / 01/07-30/09 / 01/10-31/12] - AÑO [YYYY]

### Datos del declarante
Nombre/Razón Social: [Full Legal Name]
NIF/CIF: [Your NIF]
Actividad: [Actividad económica / CNAE Code]
 epígrafe IAE: [Epígrafe(s)]

### Liquidación ( IVA REPERCUTIDO - Sales)
| Base Imponible | Tipo IVA | Cuota IVA | Total Facturado |
|----------------|----------|-----------|-----------------|
| €X,XXX.XX      | 21%      | €XXX.XX   | (auto-calc)     |
| €X,XXX.XX      | 10%      | €XX.XX    | (auto-calc)     |
| €X,XXX.XX      | 4%       | €X.XX     | (auto-calc)     |
| **TOTAL**      |          | €XXX.XX   | **€X,XXX.XX**   |

### IVA SOPORTADO - Deducible
| Concepto | Base Imponible | Tipo IVA | Cuota IVA | Cuota Deducible |
|----------|----------------|----------|-----------|-----------------|
| Bienes inversión corrientes | €XXX.XX | 21% | €XX.XX | €XX.XX |
| Resto operaciones bienes | €XXX.XX | 21% | €XX.XX | €XX.XX |
| Servicios | €XXX.XX | 21% | €XX.XX | €XX.XX |
| **TOTAL** |              |          | €XXX.XX | **€XXX.XX** |

### Regularización (si aplica)
- Biene inversión regularización: €XX.XX
- Rectificación facturas: €XX.XX
- Otros: €XX.XX

### RESULTADO LIQUIDACIÓN
| Concepto | Importe |
|----------|---------|
| IVA Repercutido | €XXX.XX |
| (-) IVA Soportado deducible | -€XXX.XX |
| (+) Regularización | +€XX.XX |
| (=) **RESULTADO** | **€XXX.XX** |

### Resultado a Ingresar / Devolver
**€XXX.XX** (a pagar a Hacienda / a devolver)
```

### Calculation Rules

| IVA Type | Repercutido (Sales) | Soportado (Purchases) | Deduction Limit |
|----------|--------------------|-----------------------|-----------------|
| 21% General | Collected from clients | Paid on expenses | 100% |
| 10% Reduced | Tourism, transport, cultural | Some services | 100% |
| 4% Super-reduced | Essential goods | Essential services | 100% |
| 0% Exento | Health, education, financial | Specific exemptions | N/A |

### Prorrata IVA (Pro-Rata)

If you perform both taxable and exempt operations:

```
## PRORRATA DE IVA
Año anterior:
- Operaciones con derecho a deducción: €XX,XXX.XX
- Operaciones exentas: €X,XXX.XX
- Total operaciones: €XX,XXX.XX
- **Prorrata general:** XX%

Aplicación en Q[X]:
- IVA soportado: €XXX.XX
- IVA deducible (aplicando prorrata): €XXX.XX
- IVA no deducible: €XX.XX
```

### Box Reference Numbers (Casillas)

| Box | Concept | Value |
|-----|---------|-------|
| 01 | Base imponible IVA 21% | €X,XXX |
| 02 | Cuota IVA 21% | €XXX |
| 03 | Base imponible IVA 10% | €X,XXX |
| 04 | Cuota IVA 10% | €XXX |
| 05 | Base imponible IVA 4% | €X,XXX |
| 06 | Cuota IVA 4% | €XXX |
| 22 | Base imponible IVA 21% (inversiones) | €X,XXX |
| 23 | Cuota IVA 21% (inversiones) | €XXX |
| 27 | IVA deducible bienes inversión | €XXX |
| 28 | IVA deducible operaciones corrientes | €XXX |
| 29 | Total IVA deducible | €XXX |
| 30 | IVA repercutido total | €XXX |
| 32 | Resultado período anterior | €XXX |
| 33 | Resultado (= 30 - 29 + 32 + regularización) | €XXX |

---

## 4. Spanish Tax Calendar (Calendario Fiscal)

### Annual Tax Calendar

| Date | Form | Period | Description |
|------|------|--------|-------------|
| **1 Jan** | - | - | Inicio año fiscal |
| **1 Jan** | - | - | Nueva cuota mínima autónomo (€230/mes) |
| **1-30 Jan** | 036/037 | 2023 | Alta/modificación censal (anual) |
| **1-30 Jan** | 100 | Nov-Dec | IRPF retenciones último trimestre |
| **1-30 Jan** | 130 | Q4 | Pago fraccionado IRPF (estimación directa) |
| **1-30 Jan** | 131 | Q4 | Pago fraccionado IRPF (módulos) |
| **1-30 Jan** | 303 | Q4 | IVA último trimestre |
| **1-30 Jan** | 390 | Anual | Resumen anual IVA |
| **1-30 Jan** | 180 | Anual | Retenciones IRPF arrendamientos |
| **1-30 Jan** | 190 | Anual | Retenciones IRPF profesionales |
| **1 Feb** | 100 | Q4 | IRPF trimestre anterior |
| **1-20 Feb** | 303 | Q4 | IVA plazo ingreso |
| **1 Feb - 31 Mar** | 100 | Anual | Declaración IRPF anterior |
| **1 Apr - 30 Jun** | 720 | Anual | Bienes en extranjero (>€50,000) |
| **1-20 Apr** | 303 | Q1 | IVA primer trimestre |
| **1-20 Apr** | 130 | Q1 | IRPF pago fraccionado Q1 |
| **1-20 Apr** | 131 | Q1 | IRPF módulos Q1 |
| **1-20 Jul** | 303 | Q2 | IVA segundo trimestre |
| **1-20 Jul** | 130 | Q2 | IRPF pago fraccionado Q2 |
| **1-20 Jul** | 131 | Q2 | IRPF módulos Q2 |
| **1-20 Oct** | 303 | Q3 | IVA tercer trimestre |
| **1-20 Oct** | 130 | Q3 | IRPF pago fraccionado Q3 |
| **1-20 Oct** | 131 | Q3 | IRPF módulos Q3 |
| **1-31 Dec** | 349 | Q3 | Intrastat, operaciones intracomunitarias |
| **31 Dec** | - | - | Fin año fiscal |

### Plazos Important Dates

| Mes | Modelo | Fecha Límite |
|-----|--------|--------------|
| Enero | 100, 130, 131, 303, 390, 180, 190 | 30 de enero |
| Febrero | 303 (opcional) | 20 de febrero |
| Marzo | 100 (anual IRPF) | Hasta 31 de marzo |
| Abril | 303, 130, 131 | 20 de abril |
| Julio | 303, 130, 131 | 20 de julio |
| Septiembre | 349 (Q2) | 30 de septiembre |
| Octubre | 303, 130, 131 | 20 de octubre |
| Diciembre | 349 (Q3) | 30 de diciembre |

### 2024-2025 Key Deadlines

```
## AÑO [2024/2025] - PLAZOS FISCALES

Q4 (Oct-Dic [prev year]):
  • 30/01/2025: 303, 130, 131, 390, 180, 190, 100

Q1:
  • 20/04/2025: 303, 130, 131

Q2:
  • 20/07/2025: 303, 130, 131

Q3:
  • 20/10/2025: 303, 130, 131

Anual:
  • 31/03/2025: IRPF Modelo 100 (anual)
  • 30/06/2025: Modelo 720 (bienes extranjero)
```

---

## 5. AI Prompts for Invoices and Tax Documents

### Invoice Generation Prompts

#### Basic Invoice (Factura Simple)

```
Prompt: Generate a professional Spanish invoice (factura) with the following details:

- Emisor (Seller): [Your business name], NIF [Your NIF], Dirección: [Your address], Email: [Your email]
- Destinatario (Client): [Client name], NIF [Client NIF], Dirección: [Client address]
- Número de factura: [Serie-XXX]
- Fecha: [YYYY-MM-DD]
- Descripción: [Service/product description]
- Base imponible: €[amount]
- IVA 21%: €[amount]
- IRPF Retención [15%/7%]: -€[amount]
- Importe total: €[amount]
- Forma de pago: [Transferencia bancaria / Bizum]
- Plazo de pago: [days]
- IBAN: [Your IBAN]

Include Spanish legal requirements: NIF, número de factura, fecha, descripción detallada, base imponible, tipo y cuota de IVA, retención IRPF, importe total, fecha de cob ro.
```

#### Invoice with Multiple Line Items

```
Prompt: Create a detailed Spanish invoice with multiple line items:

EMISOR:
- Nombre/Razón Social: [Your business name]
- NIF: [Your NIF]
- Domicilio: [Your address]
- Email: [Your email]
- Teléfono: [Your phone]

DESTINATARIO:
- Nombre/Razón Social: [Client name]
- NIF/CIF: [Client NIF]
- Domicilio: [Client address]

DATOS FACTURA:
- Número: [XXX]
- Serie: [A/B/etc]
- Fecha emisión: [YYYY-MM-DD]
- Fecha operación: [YYYY-MM-DD] (if different)

LÍNEAS:
1. [Description] - [Quantity] x €[Unit price] = €[Subtotal] + IVA [21%/10%/4%]
2. [Description] - [Quantity] x €[Unit price] = €[Subtotal] + IVA [21%/10%/4%]
3. [Description] - [Quantity] x €[Unit price] = €[Subtotal] + IVA [21%/10%/4%]

SUBTOTAL: €[amount]
IVA 21%: €[amount]
IVA 10%: €[amount] (si aplica)
IVA 4%: €[amount] (si aplica)
RETENCIÓN IRPF [15%/7%]: -€[amount]
**TOTAL**: €[amount]

FORMA DE PAGO: [Transferencia / Bizum / Cash]
PLAZO: [ días]
IBAN: [Your IBAN]

INCLUIR: nota sobre derecho a deducción fiscal para el cliente, si aplica.
```

#### Credit Note (Factura Rectificativa)

```
Prompt: Generate a Spanish credit note (factura rectificativa) to correct/modify an existing invoice:

FACTURA ORIGINAL A RECTIFICAR:
- Número: [Original invoice number]
- Fecha: [Original date]
- Base imponible: €[amount]
- IVA: €[amount]
- Total: €[amount]

MOTIVO: [Error en factura / Devolución / Descuento / Cambio condiciones]

CONCEPTO RECTIFICADO:
- Descripción: [What is being corrected]
- Base imponible original: €[amount]
- IVA original: €[amount]
- Nueva base imponible: €[amount]
- Nuevo IVA: €[amount]
- DIFERENCIA: €[amount] [a devolver/al cliente]

DATOS:
- Número factura rectificativa: [R-XXX]
- Fecha: [Current date]
- Incluir referencia a factura original

NOTA: Esta factura rectificativa sustituye a la factura número [original] y debe estar identificada como tal.
```

### Tax Document Generation Prompts

#### Modelo 303 Calculation Helper

```
Prompt: Help me calculate my Modelo 303 for [Q1/Q2/Q3/Q4] [YEAR].

IVA REPERCUTIDO (IVA collected on sales):
- Servicios profesionales: Base €X,XXX.XX + IVA 21% €XXX.XX
- [Any other income categories]

IVA SOPORTADO (IVA paid on expenses):
- Suministros profesionales: Base €XXX.XX + IVA 21% €XX.XX
- Equipamiento: Base €XXX.XX + IVA 21% €XX.XX
- Software/Servicios: Base €XXX.XX + IVA 21% €XX.XX
- [Other deductible expenses]

Calculate:
1. Total IVA repercutido
2. Total IVA soportado deducible
3. Resultado (IVA repercutido - IVA soportado)
4. Determine if I owe money or am owed a refund
5. Fill in the correct AEAT Modelo 303 casillas (boxes)

Also indicate:
- Which boxes to complete
- Any special regimes that apply
- Deadline for filing
- Payment method options
```

#### Income Tax Estimation (IRPF)

```
Prompt: Help me estimate my IRPF (Impuesto sobre la Renta) for [YEAR] as a Spanish freelancer/autónomo.

INGRESOS:
- Total facturación bruta: €XX,XXX.XX
- Retenciones IRPF practicadas: -€X,XXX.XX

GASTOS DEDUCIBLES:
- Cuota autónomo (RETA): €X,XXX.XX
- Gastos deducibles documentados: €X,XXX.XX
- Amortizaciones: €XXX.XX
- Total gastos: €X,XXX.XX

RENDIMIENTO NETO:
- Ingresos - Gastos = €XX,XXX.XX

Calculate:
1. Rendimiento neto de actividades económicas
2. Applicable IRPF bands (base imponible general)
3. Estimated IRPF tax liability
4. Minus withholdings already paid (retenciones)
5. Final payment/refund estimate

Consider:
- Mínimo personal y familiar (if applicable)
- Deducciones por inicio de actividad (primeros 2 años)
- Tipos de gravamen para autónomos en estimación directa
- Pagos fraccionados realizados (modelo 130/131)

Provide a breakdown by IRPF brackets.
```

#### Tax Planning Advice Prompt

```
Prompt: Act as a Spanish tax advisor. I'm a freelance [your profession] with:

- Ingresos brutos anuales: €XX,XXX.XX
- Gastos anuales aproximados: €X,XXX.XX
- Rendimiento neto: €XX,XXX.XX
- Cuota autónomo: €XXX/mes
- Año de inicio de actividad: [YEAR] (indicar si < 2 años para incentivos)

PROBLEMA/SITUACIÓN:
[Describe your tax situation or question]

Proporciona:
1. Análisis de tu situación fiscal actual
2. Recomendaciones de optimización fiscal legal
3. Gastos que podrías estar olvidando deducir
4. Estrategias para reducir base imponible
5. Consejos sobre IVA (prorrata, regímenes especiales)
6. Planificación de flujos de caja para impuestos
7. Próximas obligaciones fiscales y plazos

Incluye referencias a normativa vigente (Ley IRPF, Reglamento IVA, etc.)
```

### Modelo 130/131 (IRPF Quarterly Payments)

```
Prompt: Help me calculate my Modelo 130/131 for [Q1/Q2/Q3/Q4] [YEAR] as an autónomo en estimación directa.

DATOS TRIMESTRALES:
- Ingresos trimestrales: €X,XXX.XX
- Gastos deducibles: €XXX.XX
- Rendimiento neto: €X,XXX.XX

CALCULAR:
1. Rendimiento neto del trimestre
2. Pago fraccionado (20% del rendimiento neto)
3. Minus pagos anteriores del año (if Q2, Q3, Q4)
4. Resultado a ingresar o a devolver

Considerar:
- Si es inicio de actividad (primeros 2 años, tipo reducido al 20%)
- Base imponible acumulativa del año
- Límites mínimos de pago

FORMULARIO:
- Casilla 01: Rendimiento neto
- Casilla 02: 20% de casilla 01
- Casilla 03: Base para cálculo (diferencia períodos)
- Casilla 04: Resultado a ingresar

Deadline: [20th of month after quarter]
```

### Annual Tax Summary Prompt

```
Prompt: Generate a comprehensive annual tax summary for Spanish autónomo [YEAR]:

RESUMEN ANUAL [YEAR]:
1. INGRESOS
   - Total facturación: €XX,XXX.XX
   - IVA repercutido: €X,XXX.XX
   - Retenciones IRPF: -€X,XXX.XX

2. GASTOS
   - Total gastos deducibles: €X,XXX.XX
   - IVA soportado: €X,XXX.XX
   - Desglose por categorías

3. RENDIMIENTO NETO
   - Ingresos - Gastos = €XX,XXX.XX

4. CUOTAS AUTÓNOMO
   - Total cuota RETA: €X,XXX.XX
   - Base de cotización media

5. MODELOS PRESENTADOS
   - 303: 4 trimestres
   - 130/131: 4 trimestres
   - 100: Presentado [Sí/No]
   - 390: Presentado [Sí/No]
   - 180/190: Presentado [Sí/No]

6. LIQUIDACIONES
   - Total IVA a ingresar/devolver
   - Total IRPF a ingresar/devolver

7. CONSEJOS PARA [YEAR+1]
   - Ajustes recomendados
   - Objetivos de facturación
   - Previsiones de gastos
```

### Modelo 349 (Intracommunity Operations)

```
Prompt: Help me with Modelo 349 declaration for [month/Q1/Q2/Q3/Q4] [YEAR] if I have operations with EU clients:

OPERACIONES INTRACOMUNITARIAS:
- Facturas emitidas a clientes EU: [list or total]
- Facturas recibidas de proveedores EU: [list or total]

NATURE OF OPERATIONS:
- [ ] Servicios B2B a empresas EU (inversión sujeto pasivo)
- [ ] Entregas intracomunitarias de bienes
- [ ] Adquisiciones intracomunitarias

CALCULATE:
1. Total operaciones intracomunitarias
2. Diferencia entre emits and received
3. Determine if declaration is required (umbral €50,000/year or per quarter)
4. Complete Modelo 349 boxes:
   - Casilla 01: Total operaciones
   - Casilla 02: Operaciones con inversión sujeto pasivo
   - Casilla 03: Entregas intracomunitarias
   - Casilla 04: Adquisiciones intracomunitarias

5. Note relation with Modelo 303:
   - Operations must be reported in corresponding 303 boxes (04, 08, etc.)

DEADLINE:
- Monthly declarations: 20th of following month
- Quarterly: 20th of month after quarter
- Annual (if < threshold): 30 January
```

---

## 6. Quick Reference Cheat Sheets

### IVA Rates Quick Reference

| Type | Rate | Usage |
|------|------|-------|
| General | 21% | Most goods and services |
| Reducido | 10% | Tourism, transport, cultural events, some food |
| Superreducido | 4% | Essential goods: bread, milk, books, medicines |
| Exento | 0% | Health, education, financial services, insurance |

### IRPF Retention Rates

| Situation | Rate | Notes |
|-----------|------|-------|
| First 3 years of activity | 7% | Reduced retention |
| After 3 years | 15% | Standard retention |
| Special regimes | 19-45% | Progressive brackets |

### autónomo Social Security 2024

| Contribution Base | Monthly Fee | Notes |
|-------------------|-------------|-------|
| Minimum (€752.98) | €230.00 | Minimum contribution |
| Maximum (€4,495.50) | €1,176.88 | Maximum contribution |

**Tarifa plana:** First 12 months €80/month, next 12 months €160/month (if qualifies)

### Modelo Reference Numbers

| Model | Name | Frequency |
|-------|------|-----------|
| 036/037 | Census declaration | Annual/On change |
| 100 | IRPF annual | Annual |
| 130 | IRPF quarterly (direct estimation) | Quarterly |
| 131 | IRPF quarterly (modules) | Quarterly |
| 180 | IRPF rent retention annual | Annual |
| 190 | IRPF professional retention annual | Annual |
| 303 | IVA declaration | Quarterly |
| 349 | Intracommunity operations | Monthly/Quarterly/Annual |
| 390 | Annual IVA summary | Annual |
| 720 | Foreign assets declaration | Annual |

---

## 7. Document Retention

### Retention Periods (Períodos de conservación)

| Document Type | Retention Period |
|---------------|------------------|
| Facturas emitidas | 5 years (from date of issuance) |
| Facturas recibidas | 5 years (from date received) |
| Libros contables | 6 years |
| Modelo 100/130/131 archives | 6 years |
| Modelo 303 archives | 6 years |
| Contratos | 6 years after expiration |
| Nóminas/Payroll | 10 years |
| Documentación laboral | 10 years |
| Declaraciones fiscales | 6 years |
| Justificantes de pago | 6 years |

---

## Metadata

- **Skill Name:** Freelancer Finance Spain
- **Version:** 1.0.0
- **Language:** Spanish (with English prompts)
- **Tax Year:** 2024-2025
- **Last Updated:** June 2025
- **Jurisdiction:** Spain (Estado Español)
- **Author:** Hermes Agent / CodeBlueprint

---

*This skill provides general guidance for Spanish freelance tax management. Consult with a qualified gestor administrativo or tax advisor for specific advice regarding your individual situation. Tax regulations may change; always verify current rules with official AEAT sources.*
