import sqlite3
import matplotlib.pyplot as plt

# Подключаемся к БД
conn = sqlite3.connect('car_inspection.db')
df = pd.read_sql('''
    SELECT violation_type, COUNT(*) as count 
    FROM violations 
    GROUP BY violation_type
''', conn)

# Столбчатая диаграмма нарушений
df.plot(kind='bar', x='violation_type', y='count', legend=False)
plt.title("Частота нарушений по системам")
plt.ylabel("Количество")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
