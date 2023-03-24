# Bigdata
Câu 2 Bài tập lớn Bigdata

#!/usr/bin/python3
'''reducer.py'''

import sys
count = 0
total = 0
# Khởi tạo giá trị năm, nhiệt độ
(last_year, max_temp, min_temp, avg_temp) = (None, -sys.maxsize, sys.maxsize, -sys.maxsize)
for line in sys.stdin:
  # Lấy cặp giá trị <k, v> = <year, temp> từ stdin
  (year, temp) = line.strip().split("\t")
  # Nếu năm đọc vào khác năm đang xét -> (1) đưa ra stdout năm trước đó cùng với nhiệt độ cao nhất
  if last_year != None and last_year != year:
    print("%s\t%s\t%s\t%s" % (last_year, max_temp, min_temp, int(round(total / count, 1)*10)))
    # và (2) chuyển <năm, nhiệt độ> đọc vào thành <năm, nhiệt độ> đang xét:
    (last_year, max_temp, min_temp, avg_temp) = (year, int(temp), int(temp), int(temp))
    total = avg_temp
    count = 1
  else:
    # Nếu năm đọc vào trùng với năm đang xét -> tìm nhiệt độ lớn nhất của năm đó:
    (last_year, max_temp, min_temp, avg_temp) = (year, max(max_temp, int(temp)), min(min_temp, int(temp)), int(temp))
    total += avg_temp
    count += 1

# In ra kết quả cho năm cuối cùng:
if last_year:
 print("%s\t%s\t%s\t%s" % (last_year, max_temp, min_temp, int(round(total / count, 1)*10)))
