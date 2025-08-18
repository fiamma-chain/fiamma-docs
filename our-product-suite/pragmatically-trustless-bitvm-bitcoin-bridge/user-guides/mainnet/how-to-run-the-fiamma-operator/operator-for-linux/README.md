# Operator for Linux

This comprehensive guide will help you set up and run the Fiamma Operator on Linux systems for **mainnet production**. The process involves multiple steps with advanced security features including GPG-encrypted private keys.

## Production Linux Deployment

This guide is specifically designed for **production mainnet deployment** on Linux systems. All production operators must use Linux-based infrastructure for optimal security, performance, and reliability.

## Production Environment Overview

This guide covers **mainnet production deployment** with:
- **Real Bitcoin transactions** and stakes
- **Enhanced security measures** including GPG encryption
- **24/7 operational requirements**
- **Production-grade monitoring and logging**
- **Advanced troubleshooting procedures**

## Setup Process Overview

The production setup involves these key components:

1. **[Set Up Fiamma Operator](1.-set-up-fiamma-operator.md)** - Environment preparation and installation
2. **[Start and Register](2.-start-and-register.md)** - Service configuration and operator registration
3. **[Deposit and Stake](3.-deposit-and-stake.md)** - Real Bitcoin staking for production
4. **[Query Operator Status](4.-query-operator-status.md)** - Monitoring and status management
5. **[Manage the Operator Program](5.-manage-the-operator-program.md)** - Maintenance and updates
6. **[Advanced Security Setup](6.-advanced-security-setup.md)** - GPG encryption and enhanced security
7. **[Pause and Quit](7.-pause-and-quit.md)** - Graceful shutdown procedures
8. **[Troubleshooting](8.-troubleshooting.md)** - Production issue resolution

## 🔐 New Security Features

### GPG-Encrypted Private Keys
- **Enhanced security** for private key storage
- **Automatic agent caching** for seamless operation
- **Production-grade encryption** with long-term key storage
- **Compatible with systemd** auto-restart capabilities

### Benefits
- **Keys encrypted at rest** using GPG
- **Automatic decryption** via gpg-agent cache
- **Supports 24/7 operation** with automatic restarts
- **Maintains compatibility** with existing plaintext workflow

## System Requirements

### Minimum Specifications
- **OS**: Ubuntu 20.04 LTS or later (recommended), CentOS 8+, or similar
- **CPU**: 4 cores minimum (8+ recommended for production)
- **RAM**: 8GB minimum (16GB+ recommended)
- **Storage**: 100GB SSD minimum (500GB+ recommended)
- **Network**: Stable internet with low latency

### Recommended Production Setup
- **Cloud deployment**: AWS, GCP, Azure, or equivalent
- **Dedicated instance**: No shared resources
- **SSD storage**: Fast I/O for database operations
- **Monitoring**: CloudWatch, DataDog, or similar
- **Backup**: Automated backup strategy

## Security Considerations

### Production Security Requirements
- **Hardware Security Module (HSM)** support for key management
- **Multi-signature wallets** for high-value operations
- **Regular security audits** and updates
- **Intrusion detection systems** monitoring
- **Network security** with proper firewall configuration

### Data Protection
- **Encrypted storage** for all sensitive data
- **Secure backup procedures** with encryption
- **Access control** with role-based permissions
- **Audit logging** for all operations

## Pre-Installation Checklist

Before starting the installation:

✅ **Production environment** properly configured  
✅ **Security measures** in place and tested  
✅ **Backup procedures** established and verified  
✅ **Monitoring systems** ready for deployment  
✅ **Emergency procedures** documented  
✅ **Team contacts** available for 24/7 support  
✅ **Real Bitcoin** secured for staking requirements  
✅ **Production invite codes** obtained from Fiamma team  

## Getting Started

1. **Review all documentation** thoroughly before beginning
2. **Complete security assessment** of your environment
3. **Test procedures** in a staging environment if possible
4. **Follow the step-by-step guides** in order
5. **Contact support** for production-specific questions

## Support and Resources

### Production Support
- **Priority support channels** for production issues
- **24/7 emergency contacts** for critical problems
- **Technical consultation** for complex configurations
- **Security advisory** services available

### Community Resources
- **Documentation updates** regularly published
- **Best practices** shared by operator community
- **Security bulletins** for important updates
- **Performance optimization** guides

---

**⚠️ Production Warning**: This guide involves real Bitcoin transactions with significant financial implications. Ensure you fully understand all procedures, risks, and requirements before proceeding. Test thoroughly in non-production environments when possible.
