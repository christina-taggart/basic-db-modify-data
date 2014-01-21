INSERT INTO voters(id, first_name, last_name, gender, party, party_duration, age, married, children_count, homeowner, employed, created_at, updated_at)
VALUES(10001, 'Eli', 'Shurkin', 'male', 'communist', 10, 23, 0, 0, 0, 0, DATETIME('now'), DATETIME('now'));

INSERT INTO voters(id, first_name, last_name, gender, party, party_duration, age, married, children_count, homeowner, employed, created_at, updated_at)
VALUES(10002, 'John', 'Olmsted', 'male', 'communist', 15, 23, 0, 0, 0, 0, DATETIME('now'), DATETIME('now'));

INSERT INTO votes(id, voter_id, politician_id, created_at, updated_at)
VALUES(10001, 10001, 145, DATETIME('now'), DATETIME('now'));

INSERT INTO votes(id, voter_id, politician_id, created_at, updated_at)
VALUES(10002, 10002, 499, DATETIME('now'), DATETIME('now'));

UPDATE congress_members SET name='Sen. Donald Trump' WHERE id=463;

DELETE FROM voters WHERE id IN(SELECT id FROM voters WHERE party NOT IN('republican', 'democrat'));

DELETE FROM voters WHERE voters.id IN
(SELECT voters.id FROM voters
JOIN votes ON voters.id=voter_id
JOIN congress_members ON congress_members.id = politician_id
WHERE homeowner=1
AND employed=1
AND children_count=0
AND party_duration < 3
AND grade_current > 12);

UPDATE votes
SET politician_id=346
WHERE voter_id IN
(SELECT voters.id FROM voters
JOIN votes ON voters.id = voter_id
WHERE age > 80
AND children_count = 0
AND gender = 'male');

grade_1996=(SELECT MAX(grade_1996) FROM votes
JOIN congress_members ON congress_members.id = politician_id);

UPDATE votes SET politician_id =
(SELECT politician_id FROM votes
JOIN congress_members ON congress_members.id = politician_id
WHERE grade_1996=
(SELECT MIN(grade_1996) FROM votes
JOIN congress_members ON congress_members.id = politician_id))
WHERE
politician_id=(SELECT politician_id FROM votes
JOIN congress_members ON congress_members.id = politician_id
ORDER BY grade_1996 DESC
LIMIT 1);