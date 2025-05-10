# Micro_IT_FileEncryption-DecryptionTool_Project
A File Encryption and Decryption Tool is a software application that secures data by converting files into an unreadable format (encryption) and restoring them to their original form (decryption) using a key or password. This project demonstrates basic cryptography and file handling techniques.



import PyPDF2
import os

def lock_pdf(input_path, output_path, password):
    with open(input_path, 'rb') as input_file:
        pdf_reader = PyPDF2.PdfReader(input_file)
        pdf_writer = PyPDF2.PdfWriter()

        for page_num in range(len(pdf_reader.pages)):
            pdf_writer.add_page(pdf_reader.pages[page_num])

        pdf_writer.encrypt(password)

        with open(output_path, 'wb') as output_file:
            pdf_writer.write(output_file)
        print("PDF locked successfully.")

def unlock_pdf(input_path, output_path, password):
    with open(input_path, 'rb') as input_file:
        pdf_reader = PyPDF2.PdfReader(input_file)

        if pdf_reader.is_encrypted:
            try:
                pdf_reader.decrypt(password)
                pdf_writer = PyPDF2.PdfWriter()

                for page_num in range(len(pdf_reader.pages)):
                    pdf_writer.add_page(pdf_reader.pages[page_num])

                with open(output_path, 'wb') as output_file:
                    pdf_writer.write(output_file)
                print("PDF unlocked successfully.")
            except:
                print("Failed to decrypt. Wrong password?")
        else:
            print("PDF is not encrypted.")

input_file_path = r"D:\FileEncryptor\TECHNOLOGY.pdf"
locked_file_path = r"D:\FileEncryptor\\TECHNOLOGY_locked.pdf"
unlocked_file_path = r"D:\FileEncryptor\\TECHNOLOGY_unlocked.pdf"

lock_pdf(input_file_path, locked_file_path, "12345")
unlock_pdf(locked_file_path, unlocked_file_path, "12345")
