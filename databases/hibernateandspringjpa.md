---
layout: default
title: " Hibernate vs Spring Data JPA"
pagination:
  enabled: true
tags:
  - "#ORM"
  - "#DB"
---
---
## Hibernate னும் Spring JPA வும் ஒன்றா?

![[Pasted image 20251217083229.png]]

**

ORM framework என்பது Java object (Entity class)களை database table-களுடன் connect பண்ணி,

நாம எந்த ஒரு SQL லும் எழுதாமல் database லில் store / retrieve / update / delete செய்ய உதவும் framework.

Spring ecosystem லில் Entity class இல்லை. ஏன் என்றால் Spring ORM framework இல்லை. 

Hibernate தான் OG ORM framework. 

Hibernate தான் SQL ஐ generate செய்யும். 

Hibernate தான் Execute செய்யும் 

Hibernate தான் Entity Manager உதவியுடன் data வை persist செய்யும். 

Hibernate தான் மொத்த Entity life cycle ஐ manage செய்கிறது. 

Spring Data JPA என்பது, JPA Specification மட்டுமே. அதாவது JPA வின் மேல் எழுதப்பட்டிருக்கும் ஒரு Abstraction layer தான். (சுருக்கமா சொல்லனும்னா, அண்ணனுக்கு ஒத்தாசைக்கு என்பது போல..) 

உதாரணமாக, கீழே உள்ள code snippet ஐ Spring Data JPA தான் generate பண்ணும். ஆனால் Hibernate தான் Execute செய்யும். 

`public interface NoteRepository extends JPARepositories<Note, Long> {` 

`List<Note> findByStatus(String status);` 

`}` 

Your code → Spring Data JPA → JPA Specification → Hibernate → Database.

**

---

## 🔍 Important Note

<div style="overflow-x:auto;">

| Spring / Hibernate | Meaning |
|-------------------|---------|
| Spring            | Framework |
| JPA               | Specification |
| Hibernate         | JPA Implementation |

</div>

எனவே தான் **spring-boot-starter-data-jpa** dependency,
Hibernate-ஐ default-ஆ include செய்கிறது.

---

## 🍽️ Real-world Example

<div style="overflow-x:auto;">

| Role | Example |
|-----|--------|
| Menu | JPA |
| Waiter | Spring Data JPA |
| Chef | Hibernate |
| Kitchen | Database |

</div>

---

## ✅ Conclusion

- **Waiter (Spring Data JPA)** → order எடுக்கும்  
- **Chef (Hibernate)** → cook பண்ணும்  
- **Kitchen (Database)** → actual work நடக்கும்
