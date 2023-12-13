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

```sql
SELECT `students`.`surname` , `students`.`name` , `degrees`.*
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
ORDER BY `students`.`surname` ASC , `students`.`name` ASC;
```

**5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti**

```sql
SELECT `degrees`.`name` , `courses`.`name` AS `course`, `teachers`.`name` AS `teacher_name`,`teachers`.`surname` AS `teacher_surname`
FROM `degrees`
JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher`
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`

```

**6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)**

```sql
SELECT DISTINCT `teachers`.*
FROM `teachers`
JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = "Dipartimento di Matematica"

```

**7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.**

```sql
SELECT `students`.`name`, `students`.`surname`,COUNT(`students`.`id`=`exam_student`.`student_id` AND `exams`.`id`=`exam_student`.`exam_id`) AS `num_of_attempts`, MAX(`exam_student`.`vote`)
FROM `students`
JOIN `exam_student`
ON `exam_student`.`student_id` = `students`.`id`
JOIN `exams`
ON `exam_student`.`exam_id` = `exams`.`id`
GROUP BY `students`.`id`
HAVING `exam_student`.`vote`>= 18

```
