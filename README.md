#include <stdio.h>

void display_menu() {
    printf("\n=============================\n");
    printf("       الآلة الحاسبة بلغة C     \n");
    printf("=============================\n");
    printf("  العمليات المتاحة:\n");
    printf("  +  الجمع\n");
    printf("  -  الطرح\n");
    printf("  *  الضرب\n");
    printf("  /  القسمة\n");
    printf("  %%  النسبة المئوية\n");
    printf("  q  للخروج\n");
    printf("=============================\n");
}

double calculate(double a, double b, char op, int *error) {
    *error = 0;
    switch (op) {
        case '+': return a + b;
        case '-': return a - b;
        case '*': return a * b;
        case '/':
            if (b == 0) {
                printf("  خطأ: لا يمكن القسمة على صفر!\n");
                *error = 1;
                return 0;
            }
            return a / b;
        case '%':
            if (b == 0) {
                printf("  خطأ: لا يمكن القسمة على صفر!\n");
                *error = 1;
                return 0;
            }
            return (int)a % (int)b;
        default:
            printf("  خطأ: عملية غير معروفة!\n");
            *error = 1;
            return 0;
    }
}

int main() {
    double a, b, result;
    char op;
    int error;

    display_menu();

    while (1) {
        printf("\nأدخل العملية الحسابية (مثال: 5 + 3) أو (q) للخروج:\n> ");

        /* قراءة المدخلات */
        if (scanf(" %lf %c %lf", &a, &op, &b) == 3) {
            result = calculate(a, b, op, &error);
            if (!error) {
                printf("  النتيجة: %.2lf %c %.2lf = %.2lf\n", a, op, b, result);
            }
        } else {
            /* التحقق من أمر الخروج */
            char cmd;
            scanf(" %c", &cmd);
            if (cmd == 'q' || cmd == 'Q') {
                printf("\n  شكراً لاستخدام الآلة الحاسبة!\n\n");
                break;
            } else {
                printf("  خطأ: مدخل غير صحيح. حاول مرة أخرى.\n");
                /* تنظيف المدخلات */
                while (getchar() != '\n');
            }
        }
    }

    return 0;
}
