import java.util.Scanner;

public class SJF {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n;
        float avgtat = 0, avgwt = 0;

        System.out.println("Enter the number of processes:");
        n = scanner.nextInt();

        int[] pr = new int[n];
        int[] at = new int[n];
        int[] bt = new int[n];
        int[] ct = new int[n];
        int[] tat = new int[n];
        int[] wt = new int[n];
        int[] rt = new int[n];

        for (int i = 0; i < n; i++) {
            pr[i] = i + 1;
            System.out.println("Enter the arrival time of process " + (i + 1) + ":");
            at[i] = scanner.nextInt();
            System.out.println("Enter the burst time of process " + (i + 1) + ":");
            bt[i] = scanner.nextInt();
        }

        for (int i = 0; i < n - 1; i++) {
            boolean swapped = false;
            for (int j = 0; j < n - i - 1; j++) {
                if (at[j] > at[j + 1]) {
                    swap(at, j, j + 1);
                    swap(bt, j, j + 1);
                    swap(pr, j, j + 1);
                    swapped = true;
                }
            }
            if (!swapped) {
                break;
            }
        }

        ct[0] = 0;
        for (int i = 0; i < n; i++) {
            if (ct[i] < at[i]) {
                ct[i] = at[i];
            }
            ct[i] = ct[i] + bt[i];
            if (i < n - 1) {
                ct[i + 1] = ct[i];
            }
        }

        for (int i = 0; i < n; i++) {
            tat[i] = ct[i] - at[i];
            wt[i] = tat[i] - bt[i];
            rt[i] = wt[i];
        }

        System.out.println("Pr   at   bt   ct   tat   wt   rt");
        for (int i = 0; i < n; i++) {
            System.out.printf("%2d   %2d   %2d   %2d    %2d   %2d   %2d%n", pr[i], at[i], bt[i], ct[i], tat[i], wt[i], rt[i]);
            avgtat += tat[i];
            avgwt += wt[i];
        }

        System.out.println("Avgtat = " + avgtat / n);
        System.out.println("Avgwt = " + avgwt / n);
    }

    private static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }
}
