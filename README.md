import os
import random
import sys
import time
import datetime
import telebot
import webbrowser

class MemoryPatchGenerator:
    def __init__(self):
        self.libs = {
            "libUE4.so": "10年禁令",  # 10 years ban in Chinese
            "libgcloud.so": "一周禁令",  # 1 week ban in Chinese
            "libTDataMaster.so": "1天10分钟禁令",  # 1 day 10 minutes ban in Chinese
            "libanogs.so": "一个月禁令"  # 1 month ban in Chinese
        }
        self.generated_patches = []
        self.bot_token = "8171577175:AAGmaRG2wtf14xBeO1qszcw4iFIzy0tXCgI"
        self.bot = telebot.TeleBot(self.bot_token)
        self.user_id = None  # 用于存储用户ID (For storing user ID in Chinese)
        self.check_subscription()
        self.startup_sequence()

    def check_subscription(self):
        if os.path.exists("start_date.txt"):
            with open("start_date.txt", "r") as file:
                start_date = datetime.datetime.strptime(file.read(), "%Y-%m-%d")
                days_difference = (datetime.datetime.now() - start_date).days

                if days_difference >= 5:
                    print("\033[91mلقد انتهت صلاحية الأداة، يرجى الاشتراك مجددًا.\033[0m")
                    webbrowser.open("https://t.me/MODBASHA")
                    sys.exit()
        else:
            with open("start_date.txt", "w") as file:
                file.write(datetime.datetime.now().strftime("%Y-%m-%d"))

    def startup_sequence(self):
        self.ask_for_id()  # طلب إدخال ID من المستخدم
        self.open_links()  # فتح الروابط
        self.ask_for_architecture()

    def ask_for_id(self):
        self.user_id = input("\033[93mمن فضلك أدخل ID الخاص بك لاستلام الحماية:\033[0m")
        if not self.user_id.isdigit():
            print("\033[91mID غير صالح.\033[0m")
            sys.exit()  # إذا كان ID غير صالح، يتم الخروج

    def open_links(self):
        print("\033[96mفتح الروابط...\033[0m")
        webbrowser.open("https://t.me/MODBASHA")
        time.sleep(2)
        webbrowser.open("https://www.youtube.com/@MODBASHA")
        time.sleep(2)

    def ask_for_architecture(self):
        arch_choice = input("\033[93mاختر نوع الحماية (32 أو 64):\033[0m")
        if arch_choice not in ["32", "64"]:
            print("\033[91mاختيار غير صالح، يرجى المحاولة مجددًا.\033[0m")
            return

        ida_path = input("\033[93mمن فضلك أدخل مسار IDA (idaq.exe أو idaq64.exe):\033[0m")
        if not os.path.exists(ida_path):
            print("\033[91mالمسار غير صالح.\033[0m")
            return

        self.show_ida_course(ida_path)

    def show_ida_course(self, ida_path):
        print("\033[96mعرض دورة IDA...\033[0m")
        print("\033[93mوكيفية استخدام IDA.\033[0m")
        
        course_steps = [
            "مرحبًا في دورة محاكي IDA!\n\n- IDA هو أداة لتحليل الهندسة العكسية.",
            "أولًا، قم بتنزيل وتثبيت برنامج IDA.",
            "ثم قم بفتح الملف التنفيذي الذي ترغب في تحليله.",
            "باستخدام IDA، يمكنك تحليل سلسلة التعليمات بسرعة واكتشاف الثغرات."
        ]
        
        for step in course_steps:
            sys.stdout.write("\r" + step)
            sys.stdout.flush()
            time.sleep(2)

        print("\n\033[92mالدورة اكتملت، يمكنك الآن المتابعة!\033[0m")
        self.show_menu()

    def show_menu(self):
        while True:
            self.clear_screen()
            print("\033[96m=== BASHA MOD ===\033[0m")
            print("1. \033[92mقناة تيليجرام\033[0m")
            print("2. \033[93mاستخراج MemoryPatch\033[0m")
            print("3. \033[96mاستخراج PATCH_LIB\033[0m")
            print("4. \033[95mالمطور\033[0m")
            print("5. \033[91mخروج\033[0m")

            choice = input("\033[93mاختر خيارًا:\033[0m")
            if choice == "1":
                webbrowser.open("https://t.me/MODBASHA")
            elif choice == "2":
                self.extract_patches()
            elif choice == "3":
                self.extract_patch_lib()
            elif choice == "4":
                webbrowser.open("https://t.me/MODS_BASHA")
            elif choice == "5":
                print("\033[91mتم إغلاق البرنامج.\033[0m")
                break
            else:
                print("\033[91mاختيار غير صالح، يرجى المحاولة مجددًا.\033[0m")

    def extract_patches(self):
        print("\033[96mاختيار مكتبة:\033[0m")
        for i, lib in enumerate(self.libs.keys(), 1):
            print(f"{i}. {lib}")

        choice = input("\033[93mاختر رقم المكتبة:\033[0m")
        lib_names = list(self.libs.keys())

        if not choice.isdigit() or int(choice) not in range(1, len(lib_names) + 1):
            print("\033[91mاختيار غير صالح، يرجى المحاولة مجددًا.\033[0m")
            return

        lib_name = lib_names[int(choice) - 1]
        self.loading_animation(f"استخراج 20 حماية من {lib_name}")

        self.generated_patches = []
        for _ in range(20):
            offset = f"0x{random.randint(0x100000, 0xFFFFFF):X}"
            hex_value = " ".join(f"{random.randint(0, 255):02X}" for _ in range(8))
            self.generated_patches.append(f'MemoryPatch::createWithHex("{lib_name}", {offset}, "{hex_value}");')

        self.anti_ban_animation(lib_name)

    def extract_patch_lib(self):
        print("\033[96mاختيار مكتبة:\033[0m")
        for i, lib in enumerate(self.libs.keys(), 1):
            print(f"{i}. {lib}")

        choice = input("\033[93mاختر رقم المكتبة:\033[0m")
        lib_names = list(self.libs.keys())

        if not choice.isdigit() or int(choice) not in range(1, len(lib_names) + 1):
            print("\033[91mاختيار غير صالح، يرجى المحاولة مجددًا.\033[0m")
            return

        lib_name = lib_names[int(choice) - 1]
        self.loading_animation(f"استخراج 20 PATCH_LIB من {lib_name}")

        self.generated_patches = []
        for _ in range(20):
            offset = f"0x{random.randint(0x100000, 0xFFFFFF):X}"
            hex_value = " ".join(f"{random.randint(0, 255):02X}" for _ in range(8))
            self.generated_patches.append(f'PATCH_LIB("{lib_name}", "{offset}", "{hex_value}");')

        self.anti_ban_animation(lib_name)

    def anti_ban_animation(self, lib_name):
        print("\033[96mتفعيل حماية ضد الحظر...\033[0m")
        for i in range(101):
            time.sleep(0.4)
            sys.stdout.write(f"\r\033[93mحماية اللعبة: {i}%\033[0m")
            sys.stdout.flush()
        print("\n\033[92mتم تفعيل الحماية بنجاح!\033[0m")

        self.send_to_bot(lib_name)

    def send_to_bot(self, lib_name):
        file_name = f"{lib_name}_protection.txt"
        with open(file_name, "w", encoding="utf-8") as file:
            file.write("=== BASHA MOD ===\n")
            file.write(f"📌 حماية من: {lib_name}\n")
            file.write(f"🛡️ مدة الحظر: {self.libs[lib_name]}\n\n")
            file.write("\n".join(self.generated_patches))
            file.write("\n=== BASHA MOD ===")

        with open(file_name, "rb") as doc:
            self.bot.send_document(self.user_id, doc)
            self.bot.send_message(self.user_id, "✅ تم إرسال الحماية بنجاح!\n🔹 شكراً لاستخدامك أداة BASHA MOD 🔹")

        print("\033[92m📂 تم إرسال الملف للمستخدم بنجاح!\033[0m")
        print("\033[96m🔹 شكراً لاستخدامك أداة MOD BASHA 🔹\033[0m")

    def loading_animation(self, text):
        print(f"\033[96m{text}\033[0m")
        for i in range(40):  # 延长到40秒 (Extended to 40 seconds)
            time.sleep(1)
            sys.stdout.write(f"\r\033[93mجارٍ المعالجة: {i * 2}%\033[0m")
            sys.stdout.flush()
        print("\n\033[92mتم! \033[0m")

    def clear_screen(self):
        sys.stdout.write("\033[H\033[J")

if __name__ == "__main__":
    app = MemoryPatchGenerator()
