import PyPDF2
def read_pdf(file_path):
    """
    读取PDF文件文本内容
    :param file_path: PDF文件路径
    :return: 提取的文本字符串
    """
    try:
        # 以二进制只读模式打开PDF
        with open(file_path, 'rb') as f:
            # 创建PDF阅读器对象
            pdf_reader = PyPDF2.PdfReader(f)
            # 获取PDF总页数
            total_pages = len(pdf_reader.pages)
            print(f"PDF总页数：{total_pages}")
            # 逐页提取文本
            full_text = ""
            for page_num in range(total_pages):
                page = pdf_reader.pages[page_num]  # 获取第page_num页（从0开始）
                page_text = page.extract_text()  # 提取当前页文本
                full_text += page_text + "\n"  # 拼接所有页文本
        return full_text
    except Exception as e:
        print(f"读取PDF失败：{e}")
        return ""
# 测试（替换为你的PDF文件路径）
if __name__ == "__main__":
    pdf_text = read_pdf("test.pdf")
    print("PDF文本内容：\n", pdf_text[:500])  # 打印前500个字符
