terraform {
    required_version = ">= 1.3.7"

    backend "s3" {
        bucket = "terraform-backend-actions"
        key = "terraform-backend-actions.tfstate"
        region = "us-west-2"
    }
}

resource "aws_budgets_budget" "cost" {
  name              = "monthly-budget"
  budget_type       = "COST"
  limit_amount      = "10"
  limit_unit        = "USD"
  time_period_end   = "2087-06-15_00:00"
  time_period_start = "2023-01-01_00:00"
  time_unit         = "MONTHLY"

  notification {
    comparison_operator        = "GREATER_THAN"
    threshold                  = 100
    threshold_type             = "PERCENTAGE"
    notification_type          = "FORECASTED"
    subscriber_email_addresses = ["xxxxxxxxx@gmail.com"]
  }
}
