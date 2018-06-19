/**
 * Copyright (c) 1987-2010 Fujian Fujitsu Communication Software Co., Ltd. All
 * Rights Reserved. This software is the confidential and proprietary
 * information of Fujian Fujitsu Communication Software Co., Ltd.
 * ("Confidential Information"). You shall not disclose such Confidential
 * Information and shall use it only in accordance with the terms of the license
 * agreement you entered into with FFCS. FFCS MAKES NO REPRESENTATIONS OR
 * WARRANTIES ABOUT THE SUITABILITY OF THE SOFTWARE, EITHER EXPRESS OR IMPLIED,
 * INCLUDING BUT NOT LIMITED TO THE IMPLIED WARRANTIES OF MERCHANTABILITY,
 * FITNESS FOR A PARTICULAR PURPOSE, OR NON-INFRINGEMENT. FFCS SHALL NOT BE
 * LIABLE FOR ANY DAMAGES SUFFERED BY LICENSEE AS A RESULT OF USING, MODIFYING
 * OR DISTRIBUTING THIS SOFTWARE OR ITS DERIVATIVES.
 */
package com.ffcs.crm2.audit;

import org.zkoss.zk.ui.Component;
import org.zkoss.zk.ui.util.GenericForwardComposer;
import org.zkoss.zkplus.spring.SpringUtil;

import com.ffcs.crm2.audit.manager.SendSMSManager;
import com.ffcs.crm2.common.context.SessionContext;
import com.ffcs.crm2.util.msg.MsgBox;

/**
 * 实体基本信息.
 * 
 * @author Ouzhf
 * @version Revision 1.0.0
 */
public class CacheComposer extends GenericForwardComposer {
    
    /**
     * 序列化.
     */
    private static final long serialVersionUID = 1L;
    
    public CacheComposer(){
        System.out.println("aaaaaaaa");
    }
    @Override
    public void doAfterCompose(final Component comp) throws Exception {
        super.doAfterCompose(comp);
    }
    
    /**
     * 消息提示框.
     */
    private final MsgBox      msgBox           = MsgBox.getMsgBox(CacheComposer.class);
    
    /**
     */
    public void onClearCrmCache() {

        // 清除session缓存
        SessionContext.clearEntitySessionCache();
        // CRMClassProvider.clear();
        msgBox.showInfo("缓存已经全部清理， 请重新登录系统！", "提示信息", null);
        
    }
    
    /**
     */
    public void onSendSMS() {
    	System.out.println("*******************Start SendSMS*************************");
		SendSMSManager sm = (SendSMSManager)SpringUtil.getBean("sendSMSManager");
		sm.sendSMS();
    }
    
}
