# Query con SELECT

**1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia**

```sql
SELECT `students`.`name`,`students`.`surname`
FROM `students`
JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```

**2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze**

```sql
SELECT `degrees`.*
FROM `degrees`
JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`level` = 'magistrale' ;
```

**3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)**

```sql
SELECT `courses`.*
FROM `course_teacher`
JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
WHERE `teachers`.`name` = 'Fulvio'
AND `teachers`.`surname` = 'Amato'
AND `teachers`.`id` = 44;
```

**4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome**  
**5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti**  
**6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)**  
**7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.**
