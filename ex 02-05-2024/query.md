## Group by

### Contare quanti iscritti ci sono stati ogni anno
- SELECT COUNT(*) AS `number_of_students`, YEAR(`enrolment_date`) AS `enrolment_year` FROM `students` GROUP BY YEAR(`enrolment_date`) ORDER BY YEAR(`enrolment_date`) DESC;
### Contare gli insegnanti che hanno l'ufficio nello stesso edificio
- SELECT COUNT(*) AS `n_teachers`, `office_address` FROM `teachers` GROUP BY `office_address` ORDER BY `n_teachers` DESC;
### Calcolare la media dei voti di ogni appello d'esame
- SELECT `exam_id` AS `exam`, AVG(`vote`) AS `average_vote` FROM `exam_student` GROUP BY `exam_id`;
### Contare quanti corsi di laurea ci sono per ogni dipartimento
- SELECT `department_id`, COUNT(*) AS `degrees_number` FROM `degrees` GROUP BY `department_id`;

## Joins
### Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT `students`.`name` AS `student_name`,`students`.`surname` AS `student_lastname`,`degrees`.`name` AS `degree_name`
FROM `students`
INNER JOIN `degrees` 
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia";

### Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT `departments`.`name` AS `department_name`,`degrees`.`name` AS `degree_name`, `degrees`.`level` AS `degree_level`
FROM `degrees`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name`= "Dipartimento di Neuroscienze" AND `degrees`.`level`="magistrale";

### Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT `teachers`.`name` AS `teacher_name`,`teachers`.`surname` AS `teacher_lastname`,`courses`.`name` AS `course_name`,`courses`.`id` AS `course_id`
FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
WHERE `teachers`.`id` = 44;

### Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT `students`.`name` AS `student_name`, `students`.`surname` AS `student_lastname`, `degrees`.`name` AS `degree_name`, `departments`.`name` AS `department`
FROM `students`
INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `student_lastname`, `student_name`;

### Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT `degrees`.`name` AS `degree_name`, `courses`.`name` AS `course_name`, `courses`.`id` AS `course_id`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_lastname`
FROM `degrees`
INNER JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`;

### Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
SELECT DISTINCT `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_lastname`, `departments`.`name` AS `department`
FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = "Dipartimento di Matematica";
<!-- DISTINCT perchè ci sono risultati doppi ma io li voglio vedere una volta sola -->

### BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.