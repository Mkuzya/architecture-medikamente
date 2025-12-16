# Список данных для защиты и меры защиты

## Классификация данных и меры защиты

| Данные | Уровень конфиденциальности | Категория | Состояние | Способы защиты | Инструменты |
|--------|---------------------------|-----------|-----------|----------------|-------------|
| **Медицинские диагнозы** | Критический | PHI | At Rest, In Transit, In Use | Шифрование (AES-256), Обфускация, Маскирование, Тегирование | Apache Atlas, Collibra, Database Encryption, TLS 1.3 |
| **Результаты анализов** | Критический | PHI | At Rest, In Transit, In Use | Шифрование (AES-256), Обфускация, Маскирование, Тегирование, Data Lineage | Apache Atlas, Collibra, Database Encryption, TLS 1.3, BigID |
| **Хронические заболевания** | Критический | PHI | At Rest, In Transit | Шифрование (AES-256), Тегирование, RBAC | Database Encryption, TLS 1.3, Apache Atlas |
| **ФИО пациентов** | Высокий | PII | At Rest, In Transit, In Use | Шифрование (AES-256), Тегирование, Маскирование для тестирования | Database Encryption, TLS 1.3, Apache Atlas, Data Masking Tools |
| **Дата рождения** | Высокий | PII | At Rest, In Transit | Шифрование (AES-256), Тегирование | Database Encryption, TLS 1.3 |
| **Телефон** | Высокий | PII | At Rest, In Transit | Шифрование (AES-256), Тегирование, Обфускация | Database Encryption, TLS 1.3, Apache Atlas |
| **Электронная почта** | Высокий | PII | At Rest, In Transit | Шифрование (AES-256), Тегирование | Database Encryption, TLS 1.3 |
| **Адрес прописки** | Высокий | PII | At Rest, In Transit | Шифрование (AES-256), Тегирование | Database Encryption, TLS 1.3 |
| **Место работы/учёбы** | Высокий | PII | At Rest, In Transit | Шифрование (AES-256), Тегирование | Database Encryption, TLS 1.3 |
| **История лечения** | Высокий | PHI | At Rest, In Transit | Шифрование (AES-256), Тегирование, Data Lineage | Database Encryption, TLS 1.3, Apache Atlas |
| **Назначенные препараты** | Высокий | PHI | At Rest, In Transit | Шифрование (AES-256), Тегирование | Database Encryption, TLS 1.3 |
| **Данные о платежах** | Критический | Financial | At Rest, In Transit | Шифрование (AES-256), Токенизация, Тегирование, PCI DSS compliance | Database Encryption, TLS 1.3, Tokenization, Apache Atlas |
| **Счета и квитанции** | Высокий | Financial | At Rest, In Transit | Шифрование (AES-256), Тегирование | Database Encryption, TLS 1.3 |
| **Договоры на услуги** | Высокий | Financial, PII | At Rest, In Transit | Шифрование (AES-256), Тегирование, Цифровая подпись | Database Encryption, TLS 1.3, Digital Signature |
| **Данные о записях** | Средний | Administrative | At Rest, In Transit | Шифрование при передаче (TLS), Тегирование | TLS 1.3, Apache Atlas |
| **Расписание врачей** | Средний | Administrative | At Rest, In Transit | Шифрование при передаче (TLS), Тегирование | TLS 1.3 |
| **Журналы приёма** | Средний | Administrative, PII | At Rest, In Transit | Шифрование (AES-256), Тегирование | Database Encryption, TLS 1.3 |
| **Данные сотрудников** | Высокий | PII | At Rest, In Transit | Шифрование (AES-256), Тегирование, RBAC | Database Encryption, TLS 1.3, RBAC |
| **Зарплатные данные** | Критический | Financial, PII | At Rest, In Transit | Шифрование (AES-256), Тегирование, Строгий RBAC | Database Encryption, TLS 1.3, RBAC |
| **Налоговая информация** | Критический | Financial, PII | At Rest, In Transit | Шифрование (AES-256), Тегирование, Аудит | Database Encryption, TLS 1.3, Audit Logging |

## Обоснование необходимости защиты

### Критический уровень конфиденциальности

**Медицинские данные (PHI):**
- **Правовые требования:** Требования к защите медицинской информации (152-ФЗ, требования Минздрава)
- **Этические требования:** Врачебная тайна, конфиденциальность пациента
- **Риски:** Утечка может привести к дискриминации, шантажу, потере доверия
- **Последствия:** Штрафы, репутационные потери, судебные иски

**Финансовые данные:**
- **Правовые требования:** Требования ФНС, требования к обработке платёжных данных
- **Риски:** Финансовое мошенничество, кража личных данных
- **Последствия:** Финансовые потери, штрафы, потеря доверия клиентов

### Высокий уровень конфиденциальности

**Персональные данные (PII):**
- **Правовые требования:** 152-ФЗ "О персональных данных"
- **Риски:** Нарушение конфиденциальности, спам, фишинг
- **Последствия:** Штрафы до 18 млн рублей, репутационные потери

### Средний уровень конфиденциальности

**Административные данные:**
- **Риски:** Нарушение рабочего процесса, утечка расписания
- **Последствия:** Операционные проблемы, неудобства для пациентов

## Инструменты защиты данных

### Шифрование данных в покое (At Rest)

1. **Database Encryption:**
   - PostgreSQL: pgcrypto extension, Transparent Data Encryption (TDE)
   - ClickHouse: Encryption at rest
   - Инструменты: Oracle Database Vault, SQL Server Always Encrypted

2. **File System Encryption:**
   - Full Disk Encryption (FDE): BitLocker, LUKS
   - File-level encryption: EFS (Windows), EncFS (Linux)

3. **Cloud Storage Encryption:**
   - AWS S3: Server-side encryption (SSE)
   - Azure Blob Storage: Encryption at rest

### Шифрование данных при передаче (In Transit)

1. **TLS/SSL:**
   - TLS 1.3 для всех API коммуникаций
   - HTTPS для веб-приложений
   - Инструменты: Let's Encrypt, AWS Certificate Manager

2. **VPN:**
   - Для удалённого доступа сотрудников
   - Инструменты: OpenVPN, WireGuard, AWS VPN

3. **API Gateway:**
   - Шифрование всех API вызовов
   - Валидация API контрактов
   - Инструменты: Kong, AWS API Gateway, Azure API Management

### Шифрование данных в процессе использования (In Use)

1. **Application-level Encryption:**
   - Шифрование на уровне приложения
   - Инструменты: библиотеки шифрования (cryptography для Python, Bouncy Castle для Java)

2. **Trusted Execution Environments (TEE):**
   - Intel SGX для изолированного выполнения
   - Инструменты: Intel SGX SDK

### Обфускация данных

1. **Токенизация:**
   - Замена чувствительных данных токенами
   - Инструменты: Vault (HashiCorp), Tokenization services

2. **Скремблирование:**
   - Для тестовых данных
   - Инструменты: Custom scripts, Faker library

3. **Перемешивание:**
   - Для аналитических данных
   - Инструменты: Custom scripts

### Маскирование данных

1. **Статическое маскирование:**
   - Для тестовых сред
   - Инструменты: Oracle Data Masking, Informatica Data Masking

2. **Динамическое маскирование:**
   - Для продакшн-среды
   - Инструменты: Oracle Data Masking, Microsoft SQL Server Dynamic Data Masking

3. **Детерминированное маскирование:**
   - Для сохранения связей между данными
   - Инструменты: Custom masking algorithms

### Тегирование данных

1. **Apache Atlas:**
   - Для экосистемы Hadoop
   - Автоматическая классификация
   - Data Lineage

2. **Collibra Data Intelligence:**
   - Централизованное управление данными
   - Автоматическое тегирование
   - Визуализация потоков данных

3. **BigID:**
   - Автоматическое обнаружение конфиденциальных данных
   - Машинное обучение для классификации
   - Интеграция с различными системами

4. **OneTrust:**
   - Управление конфиденциальностью
   - Соответствие требованиям GDPR, 152-ФЗ
   - Автоматическая классификация

### Контроль доступа

1. **RBAC (Role-Based Access Control):**
   - Keycloak для управления ролями
   - Интеграция с приложениями
   - Инструменты: Keycloak, AWS IAM, Azure AD

2. **ABAC (Attribute-Based Access Control):**
   - Контроль доступа на основе атрибутов
   - Инструменты: AWS IAM Policies, Azure AD Conditional Access

3. **Zero Trust:**
   - Проверка на каждом этапе
   - Инструменты: Zero Trust frameworks

### Аудит и мониторинг

1. **Логирование:**
   - Централизованное логирование
   - Инструменты: ELK Stack (Elasticsearch, Logstash, Kibana), Splunk, Grafana Loki

2. **Мониторинг:**
   - Мониторинг доступа к данным
   - Инструменты: Prometheus, Grafana, Datadog

3. **Алертинг:**
   - Уведомления о подозрительной активности
   - Инструменты: PagerDuty, Opsgenie, AlertManager

4. **Аудит:**
   - Аудит всех операций с данными
   - Инструменты: AWS CloudTrail, GCP Audit Logs, Azure Monitor

### Data Lineage

1. **Apache Atlas:**
   - Для экосистемы Hadoop
   - Отслеживание потоков данных

2. **Collibra:**
   - Визуализация Data Lineage
   - Управление метаданными

3. **Informatica:**
   - Отслеживание преобразований данных
   - Интеграция с различными системами

## Рекомендации по внедрению

### Фаза 1 (Критичные меры - немедленно):
1. Внедрить шифрование данных в покое (AES-256)
2. Внедрить шифрование данных при передаче (TLS 1.3)
3. Реализовать RBAC для контроля доступа
4. Внедрить базовое логирование и аудит

### Фаза 2 (Важные меры - в течение 3 месяцев):
5. Внедрить систему тегирования данных (Apache Atlas или Collibra)
6. Реализовать Data Lineage
7. Внедрить маскирование данных для тестирования
8. Настроить мониторинг и алертинг

### Фаза 3 (Желательные меры - в течение 6 месяцев):
9. Внедрить автоматическое обнаружение данных (BigID)
10. Реализовать ABAC
11. Внедрить токенизацию для платёжных данных
12. Создать централизованный каталог данных

