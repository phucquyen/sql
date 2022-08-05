# sql testingsystem1
USE testingsystem;
-- q2 lấy ra tất cả các phòng ban 
SELECT*FROM `Depatment`;
-- q3 lấy ra id cua phong ban sale
SELECT DepartmentID FROM `Depatment`WHERE DepartmentName='SALE';
-- q4 lấy ra thông tin account có full name dài nhất
-- lenhth() dem so ky tu trong mot chuoi dau vao

SELECT * FROM `Account`WHERE LENGTH(FullName)=(SELECT MAX(LENGTH(FullName))FROM `Account`);
-- Q5 lấy ra thông tin account có full name dài  nhất và thuộc phòng ban có id_3
-- CACH 1
SELECT*FROM (SELECT*FROM `Account` WHERE DepartmentID='3') as ID_3
-- CACH 2 -- CTE tao ra 1 bang du lieu tam,bang du lieu nay chi dc dung trong cau truy van hien tai
SELECT*FROM `Account` WHERE DepartmentID='3'-- CTE ID_3
 WITH ID_3 AS (SELECT*FROM `Account` WHERE DepartmentID='3') 
SELECT * FROM `Account`WHERE LENGTH(FullName)=(SELECT MAX(LENGTH(FullName))FROM `ID_3`);

-- Q6 lấy tên gruop đã tạo trước ngày 20/11/2020
SELECT*FROM `Group`WHERE CreateDate<'2020-12-20 00:00:00';
-- q7 lấy ra id cua question có >=4 cau tra lo   
-- 1 DEM SO CAU TRA LOI CHO TUNG CAU HOI
-- 2 TIM RA CAU HOI CO >=4 CAU TRA LOI
 SELECT * FROM answer;
SELECT A.QuestionID, Q.Content, count(A.QuestionID)AS SL FROM answer  A
INNER JOIN question Q ON A.QuestionID =Q.QuestionID
 GROUP BY A.QuestionID
 HAVING count(A.QuestionID)>=4;
-- q8 lay ra cac ma de thi co thoi gian thi>=60phut va dc tao truoc ngay 20/11/2020 
SELECT `Code` FROM `Exam`WHERE Duration >=40 AND   CreateDate<'2021-11-20 00:00:00';
-- q9 lay ra 5 group tao gan day nhat
SELECT * FROM `group`ORDER BY createDate DESC LIMIT 5;
-- q10 dem so nhan vien thuoc department co id=2
SELECT * FROM  `Account` WHERE DepartmentID=2;
-- Q11 lay ra ten nhan vien co ten bat dau bang chu "h" va ket thuc bang chu "n"
SELECT*FROM `Account`WHERE Fullname LIKE 'h%n';
-- q12 xoa tat ca cac exam dc tao truoc ngay 13/11/2021
SELECT * FROM exam;
SET SQL_SAFE_UPDATES = 0;
DELETE FROM exam WHERE CreateDate<'2021-11-13';
-- q13 xoa tat ca cac question co noi dung bat dau bang tu cau hoi
-- SELECT * FROM question;
-- SET SQL_SAFE_UPDATES = 0;
 -- DELETE FROM question WHERE Content='hoi ve NET';


-- q14 updete thong tin cua account co id=5 thanh ten nguyen ba loc va email thanh loc.nguyenba@vti.com.vn
SELECT * FROM `account`;
UPDATE `account` SET FullName='nguyen ba loc', Email='thanh loc.nguyenba@vti.com.vn'WHERE AccountID=5;
-- q15 updete account co id=5 se thuoc group co id=4
SELECT * FROM `groupaccount`;
UPDATE `groupaccount` SET  AccountID=5    WHERE GroupID=4;
