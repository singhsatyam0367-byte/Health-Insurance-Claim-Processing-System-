
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

struct Policyholder
{
    int policy_no;
    char name[50];
    float sum_insured;
};

struct Claim
{
    int claim_no;
    int policy_no;
    float amount;
    char status[20];
};

// Function to find policyholder
int findPolicy(struct Policyholder *p, int n, int policy_no)
{
    int i;

    for(i = 0; i < n; i++)
    {
        if(p[i].policy_no == policy_no)
            return i;
    }

    return -1;
}

// Function to process claims
void processClaims(struct Policyholder *p, int n,
                   struct Claim *c, int m)
{
    int i, index;

    for(i = 0; i < m; i++)
    {
        index = findPolicy(p, n, c[i].policy_no);

        if(index == -1)
        {
            strcpy(c[i].status, "Pending");
        }
        else if(c[i].amount <= p[index].sum_insured)
        {
            strcpy(c[i].status, "Approved");
        }
        else
        {
            strcpy(c[i].status, "Rejected");
        }
    }
}

// Function to display claims
void displayClaims(struct Claim *c, int m)
{
    int i;

    printf("\n========== CLAIM DETAILS ==========\n");

    printf("\nClaim No\tPolicy No\tAmount\t\tStatus\n");

    for(i = 0; i < m; i++)
    {
        printf("%d\t\t%d\t\t%.2f\t\t%s\n",
               c[i].claim_no,
               c[i].policy_no,
               c[i].amount,
               c[i].status);
    }
}

// Function to generate report
void generateReport(struct Claim *c, int m)
{
    int i;
    int approved = 0, pending = 0, rejected = 0;

    for(i = 0; i < m; i++)
    {
        if(strcmp(c[i].status, "Approved") == 0)
            approved++;

        else if(strcmp(c[i].status, "Pending") == 0)
            pending++;

        else if(strcmp(c[i].status, "Rejected") == 0)
            rejected++;
    }

    printf("\n========== CLAIM REPORT ==========\n");

    printf("Total Claims Processed : %d\n", m);
    printf("Approved Claims        : %d\n", approved);
    printf("Pending Claims         : %d\n", pending);
    printf("Rejected Claims        : %d\n", rejected);
}

// Function to save data in file
void saveToFile(struct Claim *c, int m)
{
    FILE *fp;
    int i;

    fp = fopen("claims.txt", "w");

    if(fp == NULL)
    {
        printf("File cannot be opened!\n");
        return;
    }

    fprintf(fp, "HEALTH INSURANCE CLAIM REPORT\n\n");

    for(i = 0; i < m; i++)
    {
        fprintf(fp, "Claim No: %d\n", c[i].claim_no);
        fprintf(fp, "Policy No: %d\n", c[i].policy_no);
        fprintf(fp, "Amount: %.2f\n", c[i].amount);
        fprintf(fp, "Status: %s\n\n", c[i].status);
    }

    fclose(fp);

    printf("\nData successfully saved in claims.txt\n");
}

// Main function
int main()
{
    struct Policyholder *p;
    struct Claim *c;

    int n, m, i;

    printf("===== HEALTH INSURANCE CLAIM PROCESSING SYSTEM =====\n");

    printf("\nEnter number of policyholders: ");
    scanf("%d", &n);

    if(n <= 0)
    {
        printf("Invalid number of policyholders!\n");
        return 0;
    }

    // Dynamic memory allocation
    p = (struct Policyholder*)malloc(n * sizeof(struct Policyholder));

    if(p == NULL)
    {
        printf("Memory allocation failed!\n");
        return 0;
    }

    // Input policyholder details
    for(i = 0; i < n; i++)
    {
        printf("\nEnter details of Policyholder %d\n", i + 1);

        printf("Policy Number: ");
        scanf("%d", &p[i].policy_no);

        printf("Name: ");
        scanf(" %49[^\n]", p[i].name);

        printf("Sum Insured: ");
        scanf("%f", &p[i].sum_insured);
    }

    printf("\nEnter number of claims: ");
    scanf("%d", &m);

    if(m <= 0)
    {
        printf("Invalid number of claims!\n");
        free(p);
        return 0;
    }

    // Dynamic memory allocation for claims
    c = (struct Claim*)malloc(m * sizeof(struct Claim));

    if(c == NULL)
    {
        printf("Memory allocation failed!\n");
        free(p);
        return 0;
    }

    // Input claim details
    for(i = 0; i < m; i++)
    {
        printf("\nEnter details of Claim %d\n", i + 1);

        printf("Claim Number: ");
        scanf("%d", &c[i].claim_no);

        printf("Policy Number: ");
        scanf("%d", &c[i].policy_no);

        printf("Claim Amount: ");
        scanf("%f", &c[i].amount);
    }

    // Process all claims
    processClaims(p, n, c, m);

    // Display results
    displayClaims(c, m);

    // Generate report
    generateReport(c, m);

    // Save data in file
    saveToFile(c, m);

    // Free dynamically allocated memory
    free(p);
    free(c);

    printf("\nProgram completed successfully!\n");

    return 0;
}
