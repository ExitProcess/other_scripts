для работы с БД потребуется:

1) скачать БД -- https://github.com/ExitProcess/other_scripts/commit/ac4b73fe5cfe7329fe3d1f2501e0dd8549c28b6b
2) установить какой-нибудь инструмент для работы с базами данных SQLite, например
   DB Browser for SQLite (DB4S) -- http://sqlitebrowser.org/
   SQLite Expert -- http://www.sqliteexpert.com/

3) для получения списка ссылок с кодом состояния 404 выполнить запрос:

SELECT Link, HTTP_status_code FROM Links
WHERE HTTP_status_code = 404

(экспорт в xlsx -- https://github.com/ExitProcess/other_scripts/commit/f3193b04a81de78baf62b4a59254e44a7f5b13af)

4) для получения списка всех страниц, на которых есть ссылки 404, выполнить запрос:

SELECT a.Link, b.Link, b.HTTP_status_code
FROM Links a, Links b, Parent_child c
WHERE b.HTTP_status_code = 404
  AND a.Id = c.Parent_link 
  AND b.Id = c.Child_link  
ORDER BY 1

(экспорт в xlsx -- https://github.com/ExitProcess/other_scripts/commit/7f5496bc3eeb73bc64ed021b579e79ef5be5d3fb)

примечание:
при обработке ссылок скрипт не учитывает слэш, т.о. в таблицу добавляются и обрабатываются одинаковые урлы, например:
http://www.python.org/dev/peps/pep-0009
http://www.python.org/dev/peps/pep-0009/
на этой странице есть битая ссылка http://www.python.org/dev/peps/pep-xxxx/ , таким образом во втором запросе запись продублируется
(нужно допилить скрипт).
