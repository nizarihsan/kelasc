classDiagram
    class User {
        -userID: String
        -username: String
        -password: String
        -email: String
        -role: String
        +login(username: String, password: String): boolean
        +logout(): void
        +changePassword(newPassword: String): boolean
    }

    class Member {
        -memberID: String
        -name: String
        -address: String
        -phoneNumber: String
        -joinDate: Date
        -status: String
        +register(): boolean
        +updateProfile(): boolean
        +checkMembership(): MembershipStatus
        +viewMonthlyReport(): Report
    }

    class Staff {
        -staffID: String
        -position: String
        -workShift: String
        +registerMember(): boolean
        +checkMemberData(): Member
        +generateReport(): Report
        +processPayment(): boolean
    }

    class Manager {
        -managerID: String
        -department: String
        +viewReports(): Report[]
        +printReport(): boolean
        +manageStaff(): boolean
        +analyzeData(): Statistics
    }

    class Membership {
        -membershipID: String
        -type: String
        -startDate: Date
        -endDate: Date
        -price: float
        -status: String
        +calculateDuration(): int
        +renewMembership(): boolean
        +checkStatus(): String
        +updateStatus(): boolean
    }

    class Payment {
        -paymentID: String
        -amount: float
        -paymentDate: Date
        -paymentMethod: String
        -status: String
        +processPayment(): boolean
        +generateReceipt(): Receipt
        +validatePayment(): boolean
        +updatePaymentStatus(): boolean
    }

    class Attendance {
        -attendanceID: String
        -memberID: String
        -checkInTime: DateTime
        -checkOutTime: DateTime
        +recordCheckIn(): boolean
        +recordCheckOut(): boolean
        +calculateDuration(): Time
        +getAttendanceHistory(): Attendance[]
    }

    class Report {
        -reportID: String
        -type: String
        -dateGenerated: Date
        -period: String
        -data: Object
        +generateReport(): boolean
        +exportReport(): File
        +calculateStatistics(): Statistics
        +printReport(): boolean
    }

    class Receipt {
        -receiptID: String
        -paymentID: String
        -amount: float
        -date: Date
        -details: String
        +generateReceipt(): boolean
        +printReceipt(): boolean
        +emailReceipt(): boolean
        +validateReceipt(): boolean
    }

    class MembershipType {
        -typeID: String
        -name: String
        -duration: int
        -price: float
        -benefits: String[]
        +calculatePrice(): float
        +getBenefits(): String[]
        +updateType(): boolean
        +checkAvailability(): boolean
    }

    % Relationships
    User <|-- Member
    User <|-- Staff
    User <|-- Manager
    Member "1" -- "1..*" Membership
    Member "1" -- "0..*" Payment
    Member "1" -- "0..*" Attendance
    Staff "1" -- "0..*" Payment
    Manager "1" -- "0..*" Report
    Membership "1" -- "1" MembershipType
    Payment "1" -- "1" Receipt
    Payment "1" -- "1" Membership
    Report "1" -- "0..*" Attendance
    Report "1" -- "0..*" Payment
