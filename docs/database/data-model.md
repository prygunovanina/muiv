# Модель данных информационной системы "Делопроизводство"

## Основные сущности

### 1. Пользователи (Users)
- UserID (PK)
- Username
- PasswordHash
- FirstName
- LastName
- MiddleName
- Email
- Phone
- DepartmentID (FK)
- PositionID (FK)
- IsActive
- LastLoginDate
- CreatedDate
- UpdatedDate

### 2. Роли (Roles)
- RoleID (PK)
- RoleName
- Description
- IsActive

### 3. ПользователиРоли (UserRoles)
- UserRoleID (PK)
- UserID (FK)
- RoleID (FK)
- AssignedDate

### 4. Подразделения (Departments)
- DepartmentID (PK)
- DepartmentName
- ParentDepartmentID (FK)
- HeadUserID (FK)
- ContactInfo
- IsActive
- CreatedDate
- UpdatedDate

### 5. Документы (Documents)
- DocumentID (PK)
- RegNumber
- Title
- DocumentTypeID (FK)
- StatusID (FK)
- AuthorUserID (FK)
- CreatedDate
- UpdatedDate
- ContentPath
- Description
- Priority
- SecurityLevelID (FK)
- IsDeleted

### 6. ТипыДокументов (DocumentTypes)
- DocumentTypeID (PK)
- TypeName
- Description
- ModuleID (FK)
- IconPath
- IsActive

### 7. Доверенности (PowersOfAttorney)
- PowerOfAttorneyID (PK)
- DocumentID (FK)
- GrantorUserID (FK)
- AttorneyUserID (FK)
- PowersDescription
- StartDate
- EndDate
- IsSubstituteAllowed
- IsRevoked
- RevokeDate
- RevokeReason

### 8. Командировки (BusinessTrips)
- BusinessTripID (PK)
- DocumentID (FK)
- EmployeeUserID (FK)
- Destination
- Purpose
- StartDate
- EndDate
- FinancingSource
- IsCompleted
- ReportSubmitted
- ReportDate

### 9. Справки (Certificates)
- CertificateID (PK)
- DocumentID (FK)
- CertificateTypeID (FK)
- RequestedByUserID (FK)
- RecipientName
- PurposeOfIssue
- IssueDate
- ValidUntil
- IssuedByUserID (FK)

### 10. ЗадачиКонтроля (ControlTasks)
- TaskID (PK)
- DocumentID (FK)
- AssignedByUserID (FK)
- AssignedToUserID (FK)
- Description
- DueDate
- Priority
- StatusID (FK)
- CreatedDate
- CompletedDate
- Comments
- IsDeleted

## Ключевые взаимосвязи между сущностями

1. Пользователи - Роли: многие-ко-многим через ПользователиРоли
2. Пользователи - Подразделения: многие-к-одному
3. Документы - ТипыДокументов: многие-к-одному
4. Доверенности - Документы: один-к-одному
5. Командировки - Документы: один-к-одному
6. Справки - Документы: один-к-одному
7. ЗадачиКонтроля - Документы: многие-к-одному
8. Подразделения - Подразделения: один-ко-многим (рекурсивная связь)

## Примечания по организации данных

- Используется реляционная модель данных с PostgreSQL в качестве СУБД
- Для полнотекстового поиска дополнительно используется ElasticSearch
- Файлы документов хранятся в MinIO с ссылками на них в базе данных
- Предусмотрена возможность аудита изменений в критически важных таблицах
