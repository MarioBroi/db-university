## Group by
- Contare quanti iscritti ci sono stati ogni anno
```sql
SELECT EXTRACT(year FROM `enrolment_date`) AS `year`, COUNT(id) AS `subscriptions` 
FROM `students` 
GROUP BY EXTRACT(year FROM `enrolment_date`);
```

- Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```sql
SELECT COUNT(id) AS `n_of_teachers`, `office_address` AS `address` FROM `teachers` GROUP BY `office_address`;
```

- Calcolare la media dei voti di ogni appello d'esame
```sql
SELECT `exam_id`, AVG(`vote`) AS 'average_grades'
FROM `exam_student`
GROUP BY `exam_id`;
```

- Contare quanti corsi di laurea ci sono per ogni dipartimento
```sql
SELECT COUNT(`degrees`.`department_id`) AS `N_of_courses`, `departments`.`name` AS `Name_of_course`
FROM `departments`
JOIN `degrees` ON `departments`.`id` = `department_id`
GROUP BY `departments`.`name`;
```

## Joins
- Selezionare tutti gli studenti iscritti al 
```sql
SELECT `students`.`*`, `degrees`.`name` AS `Name_of_course`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
```

- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
```sql
SELECT `degrees`.`*` 
FROM `degrees` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
WHERE `degrees`.`level` = 'Magistrale' AND `departments`.`name` = 'Dipartimento di Neuroscienze';
```

- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```sql
SELECT `teachers`.`*`, `courses`.`name` AS 'name_of_courses'
FROM `teachers`
JOIN `course_teacher` ON `teacher_id` = `teachers`.`id`
JOIN `courses` ON `courses`.`id` = `course_id`
WHERE `teacher_id` = '44';
```

- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```sql
SELECT `students`.`name` AS `name`, `students`.`surname` AS `surname`, `degrees`.`name` AS 'course_name', `departments`.`name` AS 'department_name' 
FROM `students` 
JOIN `departments` 
JOIN `degrees` 
ORDER BY `students`.`surname`,`students`.`name`;
```

- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```sql
SELECT `degrees`.`name` AS `course_name`, `teachers`.`name` AS `Reachers_name`, `teachers`.`surname` AS `Reachers_surname`
FROM `degrees`
JOIN `teachers`;
```

- Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
```sql
SELECT DISTINCT `teachers`.`name` AS 'teacher_name', `teachers`.`surname` AS 'teacher_surname', `departments`.`name` AS 'department_name'
FROM `teachers`
JOIN `departments`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
ORDER BY `teacher_surname` ASC;
```

## BONUS: 
- Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.