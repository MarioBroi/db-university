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
- Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

- Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

- Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

- Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

- Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

- Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

## BONUS: 
- Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.